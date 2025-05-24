<script lang="ts">
  // We'll add professor data here later
</script>

<div class="container">
  <h1>Qui sommes-nous ?</h1>
  
  <div class="content">
    <section class="intro">
      <h2>Notre Mission</h2>
      <p>
        Nous sommes une équipe de professeurs passionnés par la philosophie et déterminés à rendre 
        cette discipline accessible et enrichissante pour tous les étudiants. Notre approche combine 
        rigueur académique et pédagogie innovante pour vous accompagner dans votre parcours 
        philosophique.
      </p>
    </section>

    <section class="team">
      <h2>Notre Équipe</h2>
      <div class="professors">
        <div class="professor-card">
          <div class="professor-image">
            <img src="/alexandre-derot.png" alt="Alexandre Derot" class="photo" />
          </div>
          <div class="professor-info">
            <h3>Alexandre Derot</h3>
            <p class="title">Agrégé de Philosophie, Doctorant, Polyglotte</p>
            <ul class="bio-list">
              <li>Ancien élève du Lycée Henri-IV</li>
              <li>Normalien Ulm</li>
              <li>Agrégé de Philosophie</li>
              <li>Doctorant en Philosophie</li>
              <li>Polyglotte (10 langues maîtrisées, 4 à niveau de bilinguisme)</li>
              <li>Polymathe (sciences humaines, sciences naturelles, mathématiques/logique)</li>
              <li>8 ans d'expérience de cours particuliers de Philosophie, de la 2nde à l'Agrégation</li>
              <li>7 ans d'expérience d'enseignement en établissement (Université, Lycée)</li>
              <li>+ 100 élèves accompagnés en philosophie</li>
              <li>Expertise en préparation de concours et examens</li>
              <li>Accompagnement global (méthodologie globale du travail)</li>
            </ul>
          </div>
        </div>
      </div>
    </section>
  </div>
</div>

<style>
  .container {
    max-width: 1200px;
    margin: 0 auto;
    padding: 2rem;
    background: none;
    color: var(--text-main);
  }

  h1 {
    color: var(--text-main);
    font-size: 2.5rem;
    margin-bottom: 2rem;
    text-align: center;
  }

  .content {
    max-width: 800px;
    margin: 0 auto;
  }

  section {
    margin-bottom: 3rem;
  }

  h2 {
    color: var(--text-main);
    font-size: 1.8rem;
    margin-bottom: 1.5rem;
  }

  .intro p {
    color: #a04a00;
    line-height: 1.8;
    font-size: 1.1rem;
  }

  .professors {
    display: grid;
    gap: 2rem;
  }

  .professor-card {
    background: var(--background-card);
    color: var(--text-main);
    border-radius: 12px;
    overflow: hidden;
    box-shadow: 0 2px 4px rgba(0,0,0,0.1);
    transition: transform 0.3s ease;
  }

  .professor-card:hover {
    transform: translateY(-5px);
  }

  .professor-image {
    width: 100%;
    height: 300px;
    background: #e9ecef;
    display: flex;
    align-items: center;
    justify-content: center;
  }

  .professor-image .photo {
    max-height: 100%;
    max-width: 100%;
    object-fit: cover;
    border-radius: 8px;
  }

  .professor-info {
    padding: 1.5rem;
  }

  .professor-info h3 {
    color: var(--text-main);
    font-size: 1.4rem;
    margin-bottom: 0.5rem;
  }

  .professor-info .title {
    color: var(--text-main);
    font-size: 1.1rem;
    margin-bottom: 1rem;
  }

  .bio-list {
    color: #a04a00;
    line-height: 1.6;
    font-size: 1rem;
    padding-left: 1.2em;
    margin: 0;
  }
  .bio-list li {
    margin-bottom: 0.5em;
  }

  @media (min-width: 768px) {
    .professors {
      grid-template-columns: repeat(2, 1fr);
    }
  }
</style> 