<script>
	export let name;
	export let description;
	export let url;
	export let stars;
</script>

<div class="project">
		<h3 class="project-title"><a href="{url}">{name}</a></h3>
		<p class="project-description">{description}</p>
		<span class="project-stars">⭐ {stars}</span>
</div>

<style>
	.project {
		display: flex;
		flex: 1 0 30%;
		justify-content: center;
		align-items: center;
		flex-direction: column;
		margin: 15px;
		border: solid 1px #009787;
	}

	.project-title {
		margin: 0;
		margin-top: 10px;
		font-size: 28px;
	}

	.project-title a {
		color: white;
	}

	.project-description {
		padding: 10px;
		font-size: 20px;
		text-align: center;
	}

	.project-stars {
		font-size: 22px;
	}
</style>
