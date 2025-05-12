<script lang="ts">
  import { page } from '$app/stores';
  
  type NodeType = 'video' | 'exercise';
  type Node = { type: NodeType };
  type TrackConfig = { nodes: Node[] };
  type TrackConfigs = {
    apprenti: TrackConfig;
    stratege: TrackConfig;
    excellence: TrackConfig;
  };
  
  const trackConfigs: TrackConfigs = {
    apprenti: {
      nodes: Array(5).fill({ type: 'video' })
    },
    stratege: {
      nodes: Array(20).fill(null).map((_, i) => ({ type: i % 2 === 0 ? 'video' : 'exercise' }))
    },
    excellence: {
      nodes: Array(30).fill(null).map((_, i) => ({ type: i % 2 === 0 ? 'video' : 'exercise' }))
    }
  };

  export let currentId = 1;
  export let currentType: NodeType = 'video';

  $: track = $page.params.track as keyof TrackConfigs;
  $: config = trackConfigs[track];
</script>

<div class="progress-container">
  <div class="progress-bar">
    {#each config.nodes as node, i}
      <a 
        href="/cours/{track}/{node.type}/{i + 1}" 
        class="node {node.type} {currentId === i + 1 && currentType === node.type ? 'current' : ''}"
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

<style>
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

  .node.current {
    transform: scale(1.1);
    box-shadow: 0 0 10px rgba(0,0,0,0.2);
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