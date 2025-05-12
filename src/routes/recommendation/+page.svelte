<script lang="ts">
  let step = 1;
  let classe = '';
  let classeAutre = '';
  let moyenne = 10;
  let objectif = '';
  let objectifAutre = '';

  function next() {
    if (step < 3) step += 1;
    else if (step === 3) step = 4; // allow to go to a result step if needed
  }

  function handleClasseChange(value: string) {
    classe = value;
    if (value !== 'Autre') classeAutre = '';
  }

  function handleObjectifChange(value: string) {
    objectif = value;
    if (value !== 'Autre') objectifAutre = '';
  }
</script>

<div class="recommend-container">
  <h1>Recommandation de Parcours</h1>

  {#if step === 1}
    <div class="question-block">
      <h2>En quelle classe êtes-vous ?</h2>
      <div class="choices">
        <label><input type="radio" name="classe" value="1e" bind:group={classe} on:change={() => handleClasseChange('1e')}/> 1e</label>
        <label><input type="radio" name="classe" value="Terminale" bind:group={classe} on:change={() => handleClasseChange('Terminale')}/> Terminale</label>
        <label><input type="radio" name="classe" value="Classe Préparatoire" bind:group={classe} on:change={() => handleClasseChange('Classe Préparatoire')}/> Classe Préparatoire</label>
        <label style="display: flex; align-items: center; gap: 0.5rem;">
          <input type="radio" name="classe" value="Autre" bind:group={classe} on:change={() => handleClasseChange('Autre')}/> Autre :
          <input type="text" bind:value={classeAutre} placeholder="Précisez..." class="input-autre" style="display: {classe === 'Autre' ? 'inline-block' : 'none'};" />
        </label>
      </div>
    </div>
  {/if}

  {#if step === 2}
    <div class="question-block">
      <h2>Quelle est votre moyenne en philosophie (ou français, sinon) ?</h2>
      <div class="choices">
        <input type="number" min="0" max="20" bind:value={moyenne} class="number-ticker" />
      </div>
    </div>
  {/if}

  {#if step === 3}
    <div class="question-block">
      <h2>Quelle est votre objectif final ?</h2>
      <div class="choices">
        <label><input type="radio" name="objectif" value="Passer les examens de cette année" bind:group={objectif} on:change={() => handleObjectifChange('Passer les examens de cette année')}/> Passer les examens de cette année</label>
        <label><input type="radio" name="objectif" value="Approfondir mon niveau" bind:group={objectif} on:change={() => handleObjectifChange('Approfondir mon niveau')}/> Approfondir mon niveau</label>
        <label style="display: flex; align-items: center; gap: 0.5rem;">
          <input type="radio" name="objectif" value="Autre" bind:group={objectif} on:change={() => handleObjectifChange('Autre')}/> Autre :
          <input type="text" bind:value={objectifAutre} placeholder="Précisez..." class="input-autre" style="display: {objectif === 'Autre' ? 'inline-block' : 'none'};" />
        </label>
      </div>
    </div>
  {/if}

  {#if step <= 3}
    <button class="nav-button next" on:click={next}>Suivant</button>
  {/if}
</div>

<style>
  .recommend-container {
    max-width: 600px;
    margin: 3rem auto;
    padding: 2rem;
    background: #f8f9fa;
    border-radius: 12px;
    box-shadow: 0 2px 8px rgba(0,0,0,0.04);
    text-align: center;
    position: relative;
    min-height: 400px;
  }
  h1 {
    color: #2c3e50;
    font-size: 2rem;
    margin-bottom: 2rem;
  }
  .question-block {
    margin-bottom: 2rem;
  }
  h2 {
    color: #2c3e50;
    font-size: 1.3rem;
    margin-bottom: 1.5rem;
  }
  .choices {
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    gap: 1rem;
    margin-left: 2rem;
  }
  label {
    font-size: 1.1rem;
    color: #34495e;
    display: flex;
    align-items: center;
    gap: 0.5rem;
  }
  .input-autre {
    margin-left: 0.5rem;
    padding: 0.3rem 0.7rem;
    border-radius: 5px;
    border: 1px solid #ccc;
    font-size: 1rem;
  }
  .number-ticker {
    width: 80px;
    font-size: 1.2rem;
    padding: 0.3rem 0.7rem;
    border-radius: 5px;
    border: 1px solid #ccc;
  }
  .nav-button.next {
    position: absolute;
    right: 2rem;
    bottom: 2rem;
    background: #6c757d;
    color: white;
    border: none;
    padding: 0.75rem 1.5rem;
    border-radius: 6px;
    font-size: 1rem;
    cursor: pointer;
    transition: background-color 0.3s ease;
    z-index: 10;
  }
  .nav-button.next:hover {
    background: #495057;
  }
</style> 