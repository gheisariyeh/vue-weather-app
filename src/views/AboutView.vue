<script>
export default {
  name: 'AboutView'
}
</script>

<template>
  <main class="about-page">
    <header class="about-hero">
      <p class="eyebrow">À PROPOS DU PROJET</p>

      <h1>Une météo plus simple</h1>

      <p class="hero-description">
        Découvrez les conditions météo de vos villes préférées,
        en quelques clics.
      </p>

      <div class="weather-symbol" aria-hidden="true">
        🌤️
      </div>
    </header>

    <section class="about-card">
      <div class="section-icon" aria-hidden="true">
        <span>☁️</span>
      </div>

      <h2>Notre application météo</h2>

      <p>
        Cette application permet de rechercher des villes
        et de consulter leurs conditions météorologiques actuelles.
      </p>

      <p>
        Les informations affichées comprennent la température,
        la température ressentie, l'humidité et les conditions du vent.
      </p>
    </section>

    <section class="about-card features-card">
      <p class="eyebrow">LES FONCTIONNALITÉS</p>

      <h2>Ce que vous pouvez faire</h2>

      <div class="feature-list">
        <article class="feature-item">
          <span class="feature-icon">📍</span>
          <div>
            <h3>Choisir une ville</h3>
            <p>Ajoutez des villes et sélectionnez celle qui vous intéresse.</p>
          </div>
        </article>

        <article class="feature-item">
          <span class="feature-icon">🌡️</span>
          <div>
            <h3>Consulter la météo</h3>
            <p>Retrouvez la température et les principales conditions météo.</p>
          </div>
        </article>

        <article class="feature-item">
          <span class="feature-icon">🔄</span>
          <div>
            <h3>Une navigation simple</h3>
            <p>Passez facilement de la page d'accueil à cette page de présentation.</p>
          </div>
        </article>
      </div>
    </section>

    <div class="about-action">
      <RouterLink to="/" class="back-button">
        ← Retour à l'accueil
      </RouterLink>
    </div>
  </main>
</template>

<style scoped>
.about-page {
  --ink: #183b56;
  --muted: #688196;
  --blue: #286f9b;
  --border: #e0eaf2;

  box-sizing: border-box;
  width: min(100%, 1000px);
  margin: 0 auto;
  padding: 2rem 1.25rem 3rem;
  color: var(--ink);
}

.about-page *,
.about-page *::before,
.about-page *::after {
  box-sizing: border-box;
}

.about-hero {
  position: relative;
  overflow: hidden;
  padding: clamp(2rem, 5vw, 3.5rem);
  margin-bottom: 1.5rem;
  border: 1px solid #dceaf5;
  border-radius: 26px;
  background: linear-gradient(135deg, #deefff, #e9edff);
}

.eyebrow {
  margin: 0 0 0.6rem;
  color: #507792;
  font-size: 0.72rem;
  font-weight: 800;
  letter-spacing: 0.12em;
}

.about-hero h1 {
  max-width: 650px;
  margin: 0;
  color: var(--ink);
  font-size: clamp(2rem, 5vw, 3rem);
  line-height: 1.15;
  letter-spacing: -0.04em;
}

.hero-description {
  max-width: 560px;
  margin: 1rem 0 0;
  color: #54728a;
  font-size: 1.05rem;
  line-height: 1.7;
}

.weather-symbol {
  position: absolute;
  top: 50%;
  right: clamp(1rem, 5vw, 3.5rem);
  transform: translateY(-50%);
  font-size: clamp(3.5rem, 9vw, 6rem);
}

.about-card {
  padding: clamp(1.4rem, 4vw, 2rem);
  margin-bottom: 1.25rem;
  border: 1px solid var(--border);
  border-radius: 24px;
  background: #fff;
  box-shadow: 0 12px 35px rgb(39 76 110 / 6%);
}

.section-icon {
  display: grid;
  width: 52px;
  height: 52px;
  margin-bottom: 1rem;
  place-items: center;
  border-radius: 16px;
  background: #e8f3fc;
  font-size: 1.6rem;
}

.about-card h2 {
  margin: 0 0 1rem;
  color: var(--ink);
  font-size: 1.4rem;
}

.about-card > p:not(.eyebrow) {
  color: var(--muted);
  line-height: 1.8;
}

.features-card > h2 {
  margin-bottom: 1.5rem;
}

.feature-list {
  display: grid;
  gap: 1rem;
}

.feature-item {
  display: flex;
  align-items: flex-start;
  gap: 1rem;
  padding: 1rem;
  border: 1px solid #e7eef5;
  border-radius: 16px;
  background: #f8fbfe;
}

.feature-icon {
  display: grid;
  width: 44px;
  height: 44px;
  flex-shrink: 0;
  place-items: center;
  border-radius: 13px;
  background: #e4f1fb;
  font-size: 1.3rem;
}

.feature-item h3 {
  margin: 0 0 0.4rem;
  color: var(--ink);
  font-size: 1rem;
}

.feature-item p {
  margin: 0;
  color: var(--muted);
  font-size: 0.9rem;
  line-height: 1.6;
}

.about-action {
  padding-top: 0.5rem;
}

.back-button {
  display: inline-flex;
  align-items: center;
  padding: 0.85rem 1.1rem;
  border-radius: 14px;
  background: var(--blue);
  color: #fff;
  font-weight: 650;
  text-decoration: none;
  transition: background 0.2s, transform 0.2s;
}

.back-button:hover {
  transform: translateY(-1px);
  background: #1d587d;
}

@media (max-width: 600px) {
  .about-page {
    padding: 1rem 0.85rem 2rem;
  }

  .about-hero {
    padding: 1.5rem;
    border-radius: 21px;
  }

  .weather-symbol {
    position: static;
    display: block;
    margin-top: 1rem;
    transform: none;
    font-size: 3rem;
  }

  .feature-item {
    padding: 0.85rem;
  }
}
</style>