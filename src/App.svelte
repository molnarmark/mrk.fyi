<script>
  import Project from './Project.svelte';
  import fetch from 'node-fetch';
  import * as animateScroll from 'svelte-scrollto';

  const REPO_URL = 'https://api.github.com/users/molnarmark/repos?per_page=100';

  let data;
  let totalLoaded = 6;
  let collapseActive = false;

  async function loadRepos() {
    const response = await fetch(REPO_URL);
    const body = await response.json();
    data = body
      .filter(repo => !repo.fork)
      .sort((a, b) => (a.stargazers_count < b.stargazers_count ? 1 : -1))
      .splice(0, totalLoaded)
      .map(repo => ({
        name: repo.name,
        description: repo.description,
        url: repo.html_url,
        stars: repo.stargazers_count,
      }));

      if (totalLoaded > 6) {
        setTimeout(() => collapseActive = true, 500);
      } else {
        collapseActive = false;
      }
  }

  async function loadMore() {
    totalLoaded += 3;
    await loadRepos();
    animateScroll.scrollToBottom();
  }

  async function collapse() {
    totalLoaded = 6;
    await loadRepos();
    animateScroll.scrollToTop();
  }

  function calculateAge() {
    return Math.abs(new Date(Date.now() - new Date('02/05/1997').getTime()).getUTCFullYear() - 1970);
  }

  loadRepos();
</script>

<main>
  <div class="body-waves"></div>
  <div id="intro">
    <h1><span class="wave">👋</span> Hello, I'm Mark.</h1>

    <span>I'm {calculateAge()}. I write code. Mainly <b class="javascript">JavaScript</b>.</span>
    <span>I'm many things, one of them is being a <b class="fullstack">Full Stack Developer</b>.</span>
    <span>I'm also a <b class="subl">Sublime Text</b> nerd and I tend to be interested in too many <b class="technologies">technologies</b>.</span>
    <br />
    <span>While you are here, you can check out some of my projects from
      <b><a href="https://github.com/molnarmark">GitHub</a></b> below.
    </span>
    <br />
  </div>

  <div id="projects">
    {#if data}
      {#each data as repo}
        <Project {...repo} />
      {/each}
    {/if}
  </div>

  <div style="z-index: 999">
    <button on:click={() => loadMore()}>Load more</button>
    {#if collapseActive}
      <button on:click={() => collapse()}>Collapse</button>
    {/if}
  </div>

  <span id="info">⚡Powered by <a href="http://svelte.dev">Svelte</a> &
    <a href="http://vercel.com">Vercel</a>
  </span>
</main>

<style>
  main {
    width: 100%;
  }

  #intro {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    z-index: 2;
    position: relative;
  }

  /*Highlights*/
  .javascript {
    color: #fee64c;
  }

  .fullstack {
    color: #5ba5e1;
  }

  .technologies {
    color: #e95459;
  }

  .subl {
    color: #f88530;
  }

  b {
    text-decoration: underline;
  }

  a {
    color: white;
  }

  #info {
    width: 100%;
    display: block;
    font-size: 20px;
    text-align: center;
    font-weight: bold;
    padding-top: 40px;
    background: rgb(255,0,0);
    background: linear-gradient(180deg, rgba(255,0,0,0) 0%, rgba(12,87,189,0.3) 67%);
    z-index: 5;
  }

  #projects {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    grid-row-end: 3;
    width: 80%;
    z-index: 2;
    min-height: 40vh;
  }

  button {
    background: none;
    color:  white;
    font-family: 'Dekko', sans-serif;
    font-weight: bold;
    font-size: 22px;
    background: #2072e008;
    border: solid 2px #2072e0;
    border-radius: 5px;
    -webkit-box-shadow: 0px 5px 0px 0px #2072e050;
    -moz-box-shadow: 0px 5px 0px 0px #2072e050;
    box-shadow: 0px 5px 0px 0px #2072e050;
    padding: 0 10px;
    z-index: 999;
    animation: fadeIn 2s;
    -webkit-animation: fadeIn 2s;
    -moz-animation: fadeIn 2s;
    -o-animation: fadeIn 2s;
    -ms-animation: fadeIn 2s;
    margin-bottom: 20px;
  }

  button:hover {
    background: #2072e050;
    cursor: pointer;
  }

  @media (max-width: 900px) {
    #intro {
      text-align: center;
      padding: 10px;
    }

    .wave {
      display: block;
    }

    #projects {
      display: grid;
      grid-template-columns: repeat(2, 1fr);
    }
  }

  @media (max-width: 600px) {
    #projects {
      display: grid;
      grid-template-columns: repeat(1, 1fr);
    }
  }
</style>
