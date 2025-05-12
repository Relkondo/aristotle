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
    apprenti: VideoTrack;
    stratege: VideoTrack;
    excellence: VideoTrack;
  };
  
  const videoContent: VideoTracks = {
    apprenti: {
      1: { title: 'Introduction à la philosophie', videoId: 'placeholder1' },
      2: { title: 'Les présocratiques', videoId: 'placeholder2' },
      3: { title: 'Socrate et Platon', videoId: 'placeholder3' },
      4: { title: 'Aristote', videoId: 'placeholder4' },
      5: { title: 'Conclusion et perspectives', videoId: 'placeholder5' }
    },
    stratege: {
      1: { title: 'Les origines de la philosophie grecque', videoId: 'stratege1' },
      2: { title: 'La méthode socratique', videoId: 'stratege2' },
      3: { title: 'La théorie des Idées de Platon', videoId: 'stratege3' },
      4: { title: 'La logique aristotélicienne', videoId: 'stratege4' },
      5: { title: 'L\'éthique à Nicomaque', videoId: 'stratege5' },
      6: { title: 'Le stoïcisme', videoId: 'stratege6' },
      7: { title: 'L\'épicurisme', videoId: 'stratege7' },
      8: { title: 'Le scepticisme antique', videoId: 'stratege8' },
      9: { title: 'La philosophie médiévale', videoId: 'stratege9' },
      10: { title: 'La renaissance de la philosophie', videoId: 'stratege10' }
    },
    excellence: {
      1: { title: 'Les présocratiques et la nature', videoId: 'excellence1' },
      2: { title: 'Socrate et l\'art du dialogue', videoId: 'excellence2' },
      3: { title: 'Platon et la justice', videoId: 'excellence3' },
      4: { title: 'Aristote et la métaphysique', videoId: 'excellence4' },
      5: { title: 'Le néoplatonisme', videoId: 'excellence5' },
      6: { title: 'La philosophie hellénistique', videoId: 'excellence6' },
      7: { title: 'Saint Augustin et la foi', videoId: 'excellence7' },
      8: { title: 'Saint Thomas d\'Aquin', videoId: 'excellence8' },
      9: { title: 'La philosophie de la Renaissance', videoId: 'excellence9' },
      10: { title: 'Le rationalisme cartésien', videoId: 'excellence10' },
      11: { title: 'L\'empirisme britannique', videoId: 'excellence11' },
      12: { title: 'Les Lumières', videoId: 'excellence12' },
      13: { title: 'Kant et la critique', videoId: 'excellence13' },
      14: { title: 'Hegel et la dialectique', videoId: 'excellence14' },
      15: { title: 'La philosophie contemporaine', videoId: 'excellence15' }
    }
  };

  function getContent(track: keyof VideoTracks, id: number): VideoContent {
    switch (track) {
      case 'apprenti':
        return videoContent.apprenti[id] || { title: 'Cours en préparation', videoId: 'placeholder' };
      case 'stratege':
        return videoContent.stratege[id] || { title: 'Cours en préparation', videoId: 'placeholder' };
      case 'excellence':
        return videoContent.excellence[id] || { title: 'Cours en préparation', videoId: 'placeholder' };
      default:
        return { title: 'Cours en préparation', videoId: 'placeholder' };
    }
  }

  $: track = $page.params.track as keyof VideoTracks;
  $: id = parseInt($page.params.id);
  $: content = getContent(track, id);
  
  // Simple increment/decrement for navigation
  $: nextId = id + 1;
  $: prevId = id - 1;
  
  // Check if next/prev content exists based on track
  $: hasNext = track === 'apprenti' ? 
    nextId <= 5 : 
    (track === 'stratege' ? nextId <= 20 : nextId <= 30);
  $: hasPrev = prevId >= 1;
  
  // Determine next and previous content types
  $: nextType = hasNext ? (
    track === 'apprenti' ? 'video' :
    nextId % 2 === 0 ? 'exercise' : 'video'
  ) : null;
  
  $: prevType = hasPrev ? (
    track === 'apprenti' ? 'video' :
    prevId % 2 === 0 ? 'exercise' : 'video'
  ) : null;
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
      <a href="/cours/{track}/{prevType}/{prevId}" class="nav-button prev">Précédent</a>
    {/if}
    {#if hasNext}
      <a href="/cours/{track}/{nextType}/{nextId}" class="nav-button next">Suivant</a>
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