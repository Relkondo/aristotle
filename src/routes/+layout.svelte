<script>
  import { webVitals } from '$lib/vitals';
  import { browser } from '$app/environment';
  import { page } from '$app/stores';
  import '../app.css';
  import { onMount } from 'svelte';

  let analyticsId = import.meta.env.VERCEL_ANALYTICS_ID;
  let isMenuOpen = false;

  $: if (browser && analyticsId) {
    webVitals({
      path: $page.url.pathname,
      params: $page.params,
      analyticsId
    })
  }

  function toggleMenu() {
    isMenuOpen = !isMenuOpen;
  }
</script>


<div class="layout" class:menu-open={isMenuOpen}>
	<button class="menu-button" on:click={toggleMenu}>
		<span class="menu-icon">☰</span>
	</button>
	
	<nav class="sidebar">
		<ul>
			<li><a href="/">Accueil</a></li>
			<li><a href="/cours">Cours</a></li>
			<li><a href="/profile">Profile</a></li>
			<li><a href="/preferences">Préférences</a></li>
		</ul>
	</nav>

	<main>
		<slot />
	</main>
</div>

<style>
	.layout {
		display: flex;
		min-height: 100vh;
		transition: padding-left 0.3s ease;
		padding-left: 0;
	}

	.layout.menu-open {
		padding-left: 250px;
	}

	.menu-button {
		position: fixed;
		top: 1rem;
		left: 1rem;
		z-index: 100;
		background: none;
		border: none;
		font-size: 1.5rem;
		cursor: pointer;
		padding: 0.5rem;
		transition: left 0.3s ease;
	}

	.menu-open .menu-button {
		left: 251px;
	}

	.sidebar {
		position: fixed;
		left: -250px;
		top: 0;
		width: 250px;
		height: 100vh;
		background-color: #f8f9fa;
		box-shadow: 2px 0 5px rgba(0, 0, 0, 0.1);
		transition: left 0.3s ease;
		z-index: 99;
	}

	.menu-open .sidebar {
		left: 0;
	}

	.sidebar ul {
		list-style: none;
		padding: 4rem 1rem 1rem 1rem;
		margin: 0;
	}

	.sidebar li {
		margin: 1rem 0;
	}

	.sidebar a {
		text-decoration: none;
		color: #2c3e50;
		font-size: 1.1rem;
		display: block;
		padding: 0.5rem;
		border-radius: 4px;
		transition: background-color 0.2s ease;
	}

	.sidebar a:hover {
		background-color: #e9ecef;
		color: #1a252f;
	}

	main {
		flex: 1;
		padding: 2rem;
		background-color: #ffffff;
	}
</style>
