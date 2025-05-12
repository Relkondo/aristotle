<script lang="ts">
  import { page } from '$app/stores';
  import ProgressBar from '$lib/components/ProgressBar.svelte';
  
  type VideoContent = {
    title: string;
    videoId: string;
  };

  type VideoTrack = {
    [key: number]: VideoContent;
  };

  type VideoTracks = {
    accelere: VideoTrack;
    classique: VideoTrack;
    premium: VideoTrack;
  };
  
  const videoContent: VideoTracks = {
    accelere: {
      1: { title: 'Introduction à la philosophie', videoId: 'placeholder1' },
      2: { title: 'Les présocratiques', videoId: 'placeholder2' },
      3: { title: 'Socrate et Platon', videoId: 'placeholder3' },
      4: { title: 'Aristote', videoId: 'placeholder4' },
      5: { title: 'Conclusion et perspectives', videoId: 'placeholder5' }
    },
    classique: {
      1: { title: 'Les origines de la philosophie grecque', videoId: 'classique1' },
      2: { title: 'La méthode socratique', videoId: 'classique2' },
      3: { title: 'La théorie des Idées de Platon', videoId: 'classique3' },
      4: { title: 'La logique aristotélicienne', videoId: 'classique4' },
      5: { title: 'L\'éthique à Nicomaque', videoId: 'classique5' },
      6: { title: 'Le stoïcisme', videoId: 'classique6' },
      7: { title: 'L\'épicurisme', videoId: 'classique7' },
      8: { title: 'Le scepticisme antique', videoId: 'classique8' },
      9: { title: 'La philosophie médiévale', videoId: 'classique9' },
      10: { title: 'La renaissance de la philosophie', videoId: 'classique10' }
    },
    premium: {
      1: { title: 'Les présocratiques et la nature', videoId: 'premium1' },
      2: { title: 'Socrate et l\'art du dialogue', videoId: 'premium2' },
      3: { title: 'Platon et la justice', videoId: 'premium3' },
      4: { title: 'Aristote et la métaphysique', videoId: 'premium4' },
      5: { title: 'Le néoplatonisme', videoId: 'premium5' },
      6: { title: 'La philosophie hellénistique', videoId: 'premium6' },
      7: { title: 'Saint Augustin et la foi', videoId: 'premium7' },
      8: { title: 'Saint Thomas d\'Aquin', videoId: 'premium8' },
      9: { title: 'La philosophie de la Renaissance', videoId: 'premium9' },
      10: { title: 'Le rationalisme cartésien', videoId: 'premium10' },
      11: { title: 'L\'empirisme britannique', videoId: 'premium11' },
      12: { title: 'Les Lumières', videoId: 'premium12' },
      13: { title: 'Kant et la critique', videoId: 'premium13' },
      14: { title: 'Hegel et la dialectique', videoId: 'premium14' },
      15: { title: 'La philosophie contemporaine', videoId: 'premium15' }
    }
  };

  function getContent(track: keyof VideoTracks, id: number): VideoContent {
    switch (track) {
      case 'accelere':
        return videoContent.accelere[id] || { title: 'Cours en préparation', videoId: 'placeholder' };
      case 'classique':
        return videoContent.classique[id] || { title: 'Cours en préparation', videoId: 'placeholder' };
      case 'premium':
        return videoContent.premium[id] || { title: 'Cours en préparation', videoId: 'placeholder' };
      default:
        return { title: 'Cours en préparation', videoId: 'placeholder' };
    }
  }

  function hasNextContent(track: keyof VideoTracks, id: number): boolean {
    switch (track) {
      case 'accelere':
        return !!videoContent.accelere[id + 1];
      case 'classique':
        return !!videoContent.classique[id + 1];
      case 'premium':
        return !!videoContent.premium[id + 1];
      default:
        return false;
    }
  }

  function hasPrevContent(track: keyof VideoTracks, id: number): boolean {
    switch (track) {
      case 'accelere':
        return !!videoContent.accelere[id - 1];
      case 'classique':
        return !!videoContent.classique[id - 1];
      case 'premium':
        return !!videoContent.premium[id - 1];
      default:
        return false;
    }
  }
  
  $: track = $page.params.track as keyof VideoTracks;
  $: id = parseInt($page.params.id);
  $: content = getContent(track, id);
  $: nextId = id + 1;
  $: prevId = id - 1;
  $: hasNext = hasNextContent(track, id);
  $: hasPrev = hasPrevContent(track, id);
</script>

<div class="container">
  <h1>{content.title}</h1>
  
  <div class="video-container">
    <div class="video-placeholder">
      <p>Vidéo à venir</p>
      <p class="video-id">ID: {content.videoId}</p>
    </div>
  </div>

  <div class="navigation">
    {#if hasPrev}
      <a href="/cours/{track}/video/{prevId}" class="nav-button prev">Précédent</a>
    {/if}
    {#if hasNext}
      <a href="/cours/{track}/video/{nextId}" class="nav-button next">Suivant</a>
    {/if}
  </div>

  <ProgressBar currentId={id} currentType="video" />
</div>

<style>
  .container {
    max-width: 1200px;
    margin: 0 auto;
    padding: 2rem;
  }

  h1 {
    color: #2c3e50;
    font-size: 2rem;
    margin-bottom: 2rem;
    text-align: center;
  }

  .video-container {
    margin: 2rem auto;
    max-width: 800px;
  }

  .video-placeholder {
    background-color: #f8f9fa;
    aspect-ratio: 16/9;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    border-radius: 8px;
    color: #666;
  }

  .video-id {
    font-size: 0.9rem;
    margin-top: 1rem;
    color: #999;
  }

  .navigation {
    display: flex;
    justify-content: space-between;
    margin-top: 2rem;
  }

  .nav-button {
    background: #6c757d;
    color: white;
    text-decoration: none;
    padding: 0.75rem 1.5rem;
    border-radius: 6px;
    transition: background-color 0.3s ease;
  }

  .nav-button:hover {
    background: #495057;
  }

  .nav-button.prev {
    margin-right: auto;
  }

  .nav-button.next {
    margin-left: auto;
  }
</style> 