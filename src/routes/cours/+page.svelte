<script>
  const tracks = [
    {
      id: 'apprenti',
      title: 'Apprenti',
      courses: 5,
      description: 'Un parcours intensif de 5 semaines pour maîtriser les fondamentaux de la philosophie.',
      color: '#4a6b8a',
      hoverColor: '#3a5a7a',
      path: '/cours/apprenti'
    },
    {
      id: 'stratege',
      title: 'Stratège',
      courses: 10,
      description: 'Un parcours complet de 10 semaines pour une compréhension approfondie de la philosophie.',
      color: '#5d7a6d',
      hoverColor: '#4d6a5d',
      path: '/cours/stratege'
    },
    {
      id: 'excellence',
      title: 'Excellence',
      courses: 15,
      description: 'Un parcours approfondi de 15 semaines avec des contenus exclusifs et un suivi personnalisé.',
      color: '#7a6b8a',
      hoverColor: '#6a5a7a',
      path: '/cours/excellence'
    }
  ];
</script>

<svelte:head>
  <title>Cours - Les Chemins d'Aristote</title>
</svelte:head>

<div class="container">
  <h1>Nos Parcours</h1>
  <p class="subtitle">Choisissez le parcours qui correspond le mieux à vos objectifs</p>

  <div class="tracks-grid">
    {#each tracks as track}
      <div class="track-card" style="--track-color: {track.color}; --track-hover-color: {track.hoverColor}">
        <div class="track-header">
          <h2>{track.title}</h2>
          <span class="course-count">{track.courses} cours</span>
        </div>
        <p class="track-description">{track.description}</p>
        <a href={track.path} class="enroll-button">Accéder</a>
      </div>
    {/each}
  </div>
</div>

<style>
  .container {
    max-width: 1200px;
    margin: 0 auto;
    padding: 2rem;
  }

  h1, .subtitle {
    color: var(--text-main);
  }

  h1 {
    font-size: 2.5rem;
    margin-bottom: 1rem;
    text-align: center;
  }

  .subtitle {
    text-align: center;
    margin-bottom: 3rem;
    font-size: 1.2rem;
  }

  .tracks-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
    gap: 2rem;
    padding: 1rem;
  }

  .track-card {
    background: var(--background-card);
    color: var(--text-main);
    border-radius: 12px;
    padding: 2rem;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
    transition: all 0.3s ease;
    border: 2px solid var(--track-color);
    display: flex;
    flex-direction: column;
    gap: 1.5rem;
  }

  .track-card:hover {
    background: #e6cfa7;
    color: #a04a00;
    transform: translateY(-5px);
    box-shadow: 0 8px 15px rgba(0, 0, 0, 0.1);
    border-color: var(--track-hover-color);
  }

  .track-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 1rem;
  }

  .track-header h2 {
    font-size: 1.8rem;
    margin: 0;
  }

  .course-count {
    background: var(--track-color);
    color: white;
    padding: 0.5rem 1rem;
    border-radius: 20px;
    font-size: 0.9rem;
    font-weight: 500;
  }

  .track-description {
    line-height: 1.6;
    flex-grow: 1;
  }

  .enroll-button {
    background: var(--track-color);
    color: white;
    border: none;
    padding: 1rem 2rem;
    border-radius: 6px;
    font-size: 1.1rem;
    cursor: pointer;
    transition: background-color 0.3s ease;
    text-decoration: none;
    text-align: center;
    display: inline-block;
    min-width: 120px;
  }

  .enroll-button:hover {
    background: var(--track-hover-color);
  }

  @media (max-width: 768px) {
    .tracks-grid {
      grid-template-columns: 1fr;
    }
  }
</style> 