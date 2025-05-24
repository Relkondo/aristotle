<script>
	// Video placeholder will be added later
</script>

<svelte:head>
	<title>Les Chemins d'Aristote</title>
	<meta name="description" content="Apprenez la philosophie en français" />
</svelte:head>

<div class="container">
	<h1>Les Chemins d'Aristote</h1>
	
	<div class="welcome-text">
		<p>
			Bienvenue sur Les Chemins d'Aristote, votre portail vers la philosophie en français. 
			Notre mission est de rendre la philosophie accessible à tous, à travers des cours 
			structurés, des exercices pratiques et une communauté d'apprenants passionnés.
		</p>
	</div>

	<div class="video-placeholder">
		<div class="video-container">
			<p>Vidéo à venir</p>
		</div>
	</div>

	<a href="/recommendation" class="recommend-link">Quel parcours choisir ?</a>
</div>

<style>
	.container {
		max-width: 1200px;
		margin: 0 auto;
		padding: 2rem;
		text-align: center;
		background: none;
		color: var(--text-main);
	}

	h1 {
		font-size: 3rem;
		color: var(--text-main);
		margin-bottom: 2rem;
	}

	.welcome-text, .welcome-text p {
		color: var(--text-main);
	}

	.welcome-text {
		max-width: 800px;
		margin: 0 auto 3rem auto;
		line-height: 1.6;
	}

	.welcome-text p {
		font-size: 1.2rem;
	}

	.video-placeholder {
		margin: 2rem auto;
		max-width: 800px;
	}

	.video-container {
		background: var(--background-card);
		aspect-ratio: 16/9;
		display: flex;
		align-items: center;
		justify-content: center;
		border-radius: 8px;
		color: #a04a00;
	}

	.recommend-link {
		display: inline-block;
		margin: 2rem auto 0 auto;
		padding: 1rem 2rem;
		background: var(--sidebar-link-hover);
		color: var(--text-main);
		border-radius: 8px;
		font-size: 1.1rem;
		text-decoration: none;
		transition: background 0.2s, color 0.2s;
		box-shadow: 0 2px 4px rgba(0,0,0,0.04);
		border: 1px solid #e6cfa7;
	}
	.recommend-link:hover {
		background: #fbe3c0;
		color: #a04a00;
	}
</style>
