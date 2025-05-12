<script lang="ts">
  import { page } from '$app/stores';
  
  type TrackType = 'apprenti' | 'stratege' | 'excellence';
  type NodeType = 'video' | 'exercise';
  type TrackConfig = {
    title: string;
    description: string;
    nodes: { type: NodeType }[];
  };
  type TrackConfigs = { [key in TrackType]: TrackConfig };
  
  const trackConfigs: TrackConfigs = {
    apprenti: {
      title: 'Parcours Apprenti',
      description: 'Un parcours intensif couvrant les concepts fondamentaux de la philosophie. Idéal pour une première approche ou une révision rapide.',
      nodes: Array(5).fill({ type: 'video' })
    },
    stratege: {
      title: 'Parcours Stratège',
      description: 'Un programme complet alternant cours vidéo et exercices pratiques. Approfondissez votre compréhension à travers des exercices corrigés par le professeur.',
      nodes: Array(20).fill(null).map((_, i) => ({ type: i % 2 === 0 ? 'video' : 'exercise' }))
    },
    excellence: {
      title: 'Parcours Excellence',
      description: 'Le programme le plus complet avec des entretiens personnalisés. Perfectionnez votre maîtrise de la philosophie avec un accompagnement sur mesure.',
      nodes: Array(30).fill(null).map((_, i) => ({ type: i % 2 === 0 ? 'video' : 'exercise' }))
    }
  };

  $: track = $page.params.track as TrackType;
  $: config = trackConfigs[track];
</script>

<div class="container">
  <h1>{config.title}</h1>
  <p class="description">{config.description}</p>

  <div class="progress-container">
    <div class="progress-bar">
      {#each config.nodes as node, i}
        <a 
          href="/cours/{track}/{node.type}/{i + 1}" 
          class="node {node.type}"
          title={node.type === 'video' ? 'Cours vidéo' : 'Exercice'}
        >
          {i + 1}
        </a>
        {#if i < config.nodes.length - 1}
          <div class="connector"></div>
        {/if}
      {/each}
    </div>
  </div>
</div>

<style>
  .container {
    max-width: 1200px;
    margin: 0 auto;
    padding: 2rem;
  }

  h1 {
    color: #2c3e50;
    font-size: 2.5rem;
    margin-bottom: 1rem;
    text-align: center;
  }

  .description {
    color: #666;
    text-align: center;
    margin-bottom: 4rem;
    font-size: 1.2rem;
    line-height: 1.6;
    max-width: 800px;
    margin-left: auto;
    margin-right: auto;
  }

  .progress-container {
    margin-top: 4rem;
    padding: 2rem;
    background: #f8f9fa;
    border-radius: 12px;
  }

  .progress-bar {
    display: flex;
    align-items: center;
    justify-content: center;
    flex-wrap: wrap;
    gap: 0.5rem;
  }

  .node {
    width: 40px;
    height: 40px;
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    text-decoration: none;
    color: white;
    font-weight: 500;
    transition: all 0.3s ease;
  }

  .node.video {
    background: #6c757d;
  }

  .node.exercise {
    background: #4a5568;
    clip-path: polygon(50% 0%, 100% 50%, 50% 100%, 0% 50%);
  }

  .node:hover {
    transform: scale(1.1);
  }

  .connector {
    width: 40px;
    height: 2px;
    background: #dee2e6;
  }

  @media (max-width: 768px) {
    .progress-bar {
      gap: 0.25rem;
    }

    .node {
      width: 30px;
      height: 30px;
      font-size: 0.9rem;
    }

    .connector {
      width: 20px;
    }
  }
</style> 