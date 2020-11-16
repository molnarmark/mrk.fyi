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
	<div id="intro">
		<h1>👋 Hello, I'm Mark.</h1>

		<span>I'm 23. I write code. Mainly <b color="#f9e61e">JavaScript</b>.</span>
		<span>I'm many things, one of them is being a <b color="#1f48b2">Full-Stack Developer</b>.</span>
		<span>I'm also a <b color="#F89821">Sublime Text</b> nerd and I tend to be interested in too many<b color="#b21f1f">technologies</b>.</span>
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
		background: black;
	}

	#projects {
		display: flex;
		flex-direction: row;
		justify-content: center;
		flex-wrap: wrap;
	}
</style>
