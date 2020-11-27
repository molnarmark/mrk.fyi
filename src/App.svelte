<script>
	import Project from './Project.svelte';
	import fetch from 'node-fetch';

	const REPO_URL = 'https://api.github.com/users/molnarmark/repos?per_page=100';

	let data;
	(async () => {
		const response = await fetch(REPO_URL);
		const body = await response.json();

		data = body
			.filter(repo => !repo.fork)
			.sort((a, b) => (a.stargazers_count < b.stargazers_count ? 1 : -1))
			.splice(0, 6)
			.map(repo => ({
				name: repo.name,
				description: repo.description,
				url: repo.html_url,
				stars: repo.stargazers_count,
			}));
	})();
</script>

<main>
	<div class="body-waves"></div>
	<div id="intro">
		<h1><span class="wave">👋</span> Hello, I'm Mark.</h1>

		<span>I'm 23. I write code. Mainly <b class="javascript">JavaScript</b>.</span>
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

	<span id="info">⚡Powered by <a href="http://svelte.dev">Svelte</a> &
		<a href="http://vercel.com">Vercel</a>
	</span>
</main>

<style>
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
		background: black;
	}

	#projects {
		display: flex;
		flex-direction: row;
		justify-content: center;
		flex-wrap: wrap;
		width: 80%;
		background: black;
		z-index: 2;
	}
</style>
