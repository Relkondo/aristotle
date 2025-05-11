<script>
	import Header from '$lib/header/Header.svelte';
  import { webVitals } from '$lib/vitals';
  import { browser } from '$app/env';
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

<Header />

<div class="layout">
	<button class="menu-button" on:click={toggleMenu}>
		<span class="menu-icon">☰</span>
	</button>
	
	<nav class="sidebar" class:open={isMenuOpen}>
		<ul>
			<li><a href="/cours">Cours</a></li>
			<li><a href="/profile">Profile</a></li>
			<li><a href="/preferences">Préférences</a></li>
		</ul>
	</nav>

	<main>
		<slot />
	</main>
</div>

<footer>
	<p>visit <a href="https://kit.svelte.dev">kit.svelte.dev</a> to learn SvelteKit</p>
</footer>

<style>
	.layout {
		display: flex;
		min-height: 100vh;
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
	}

	.sidebar {
		position: fixed;
		left: -250px;
		top: 0;
		width: 250px;
		height: 100vh;
		background-color: white;
		box-shadow: 2px 0 5px rgba(0, 0, 0, 0.1);
		transition: left 0.3s ease;
		z-index: 99;
	}

	.sidebar.open {
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
		color: #333;
		font-size: 1.1rem;
		display: block;
		padding: 0.5rem;
	}

	.sidebar a:hover {
		color: #666;
	}

	main {
		flex: 1;
		padding: 2rem;
	}

	footer {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		padding: 40px;
	}

	footer a {
		font-weight: bold;
	}

	@media (min-width: 480px) {
		footer {
			padding: 40px 0;
		}
	}
</style>
