<script>
  import { page } from '$app/stores';
  import ProgressBar from '$lib/components/ProgressBar.svelte';
  
  const exerciseContent = {
    accelere: {},
    classique: {
      1: { question: 'Quelle est la place de la raison dans la connaissance selon Platon ?' },
      2: { question: 'Comment Aristote définit-il le bonheur ?' },
      3: { question: 'Analysez la notion de vertu dans l\'éthique aristotélicienne.' },
      4: { question: 'Quelle est la conception du temps chez Saint Augustin ?' },
      5: { question: 'Expliquez la théorie de la connaissance de Descartes.' },
      6: { question: 'Quelle est la place de la liberté dans la philosophie de Spinoza ?' },
      7: { question: 'Analysez la notion de substance chez Leibniz.' },
      8: { question: 'Comment Kant définit-il les conditions de possibilité de la connaissance ?' },
      9: { question: 'Quelle est la conception de l\'histoire chez Hegel ?' },
      10: { question: 'Expliquez la dialectique du maître et de l\'esclave chez Hegel.' }
    },
    premium: {
      1: { question: 'Analysez la notion de justice dans la République de Platon.' },
      2: { question: 'Quelle est la relation entre l\'âme et le corps selon Descartes ?' },
      3: { question: 'Expliquez la théorie des monades de Leibniz.' },
      4: { question: 'Quelle est la conception de la liberté chez Kant ?' },
      5: { question: 'Analysez la dialectique hégélienne et son application à l\'histoire.' },
      6: { question: 'Quelle est la place de la volonté dans la philosophie de Schopenhauer ?' },
      7: { question: 'Expliquez la notion de surhomme chez Nietzsche.' },
      8: { question: 'Analysez la conception de l\'existence chez Kierkegaard.' },
      9: { question: 'Quelle est la théorie de la connaissance chez Husserl ?' },
      10: { question: 'Expliquez la notion d\'être-pour-la-mort chez Heidegger.' },
      11: { question: 'Analysez la conception de la liberté chez Sartre.' },
      12: { question: 'Quelle est la théorie de la justice chez Rawls ?' },
      13: { question: 'Expliquez la notion de pouvoir chez Foucault.' },
      14: { question: 'Analysez la conception de la démocratie chez Habermas.' },
      15: { question: 'Quelle est la place de l\'éthique dans la philosophie contemporaine ?' }
    }
  };

  const validTracks = ['accelere', 'classique', 'premium'];
  
  $: track = validTracks.includes($page.params.track) ? $page.params.track : 'accelere';
  $: id = parseInt($page.params.id);
  $: content = exerciseContent[track]?.[id] || { question: 'Exercice en préparation' };
  $: answer = '';
  $: nextId = id + 1;
  $: prevId = id - 1;
  $: hasNext = exerciseContent[track]?.[nextId];
  $: hasPrev = exerciseContent[track]?.[prevId];

  function handleSubmit() {
    // Here you would typically send the answer to a server
    console.log('Answer submitted:', answer);
    alert('Votre réponse a été enregistrée.');
  }
</script>

<div class="container">
  <h1>Exercice {id}</h1>
  
  <div class="exercise-container">
    <div class="question">
      <h2>Sujet de dissertation</h2>
      <p>{content.question}</p>
    </div>

    <form on:submit|preventDefault={handleSubmit} class="answer-form">
      <textarea
        bind:value={answer}
        placeholder="Votre réponse..."
        rows="15"
      ></textarea>
      
      <div class="form-actions">
        <button type="submit" class="submit-button">Soumettre</button>
      </div>
    </form>
  </div>

  <div class="navigation">
    {#if hasPrev}
      <a href="/cours/{track}/exercise/{prevId}" class="nav-button prev">Précédent</a>
    {/if}
    {#if hasNext}
      <a href="/cours/{track}/exercise/{nextId}" class="nav-button next">Suivant</a>
    {/if}
  </div>

  <ProgressBar currentId={id} currentType="exercise" />
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

  .exercise-container {
    max-width: 800px;
    margin: 0 auto;
  }

  .question {
    background: #f8f9fa;
    padding: 2rem;
    border-radius: 8px;
    margin-bottom: 2rem;
  }

  .question h2 {
    color: #2c3e50;
    font-size: 1.5rem;
    margin-bottom: 1rem;
  }

  .question p {
    color: #666;
    line-height: 1.6;
    font-size: 1.1rem;
  }

  .answer-form {
    display: flex;
    flex-direction: column;
    gap: 1rem;
  }

  textarea {
    width: 100%;
    padding: 1rem;
    border: 2px solid #dee2e6;
    border-radius: 8px;
    font-size: 1rem;
    line-height: 1.6;
    resize: vertical;
    transition: border-color 0.3s ease;
  }

  textarea:focus {
    outline: none;
    border-color: #6c757d;
  }

  .form-actions {
    display: flex;
    justify-content: flex-end;
  }

  .submit-button {
    background: #6c757d;
    color: white;
    border: none;
    padding: 0.75rem 1.5rem;
    border-radius: 6px;
    font-size: 1rem;
    cursor: pointer;
    transition: background-color 0.3s ease;
  }

  .submit-button:hover {
    background: #495057;
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