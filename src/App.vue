<template>
  <div class="app-shell">
    <header class="site-header">
      <RouterLink to="/" class="brand">
        <span class="brand-icon">☀️</span>
        <span>Mon<span class="brand-accent">Temps</span></span>
      </RouterLink>

      <nav class="site-nav">
        <RouterLink to="/">Accueil</RouterLink>
        <RouterLink to="/about">À propos</RouterLink>
      </nav>
    </header>

    <RouterView />

    <footer class="site-footer">
      Une météo plus simple, ville après ville.
    </footer>
  </div>
</template>

<style scoped>
.app-shell {
  min-height: 100vh;
}

.site-header {
  width: min(100% - 40px, 1000px);
  margin: 0 auto;
  padding: 1.2rem 0;
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 1rem;
  border-bottom: 1px solid #e1ebf3;
}

.brand {
  display: inline-flex;
  align-items: center;
  gap: 0.6rem;
  color: #183b56;
  text-decoration: none;
  font-size: 1.25rem;
  font-weight: 800;
}

.brand-icon {
  font-size: 1.5rem;
}

.brand-accent {
  color: #286f9b;
}

.site-nav {
  display: flex;
  gap: 0.6rem;
}

.site-nav a {
  padding: 0.65rem 0.9rem;
  border-radius: 12px;
  color: #59758b;
  text-decoration: none;
  font-size: 0.9rem;
  font-weight: 600;
}

.site-nav a:hover,
.site-nav a.router-link-active {
  background: #e4f1fb;
  color: #286f9b;
}

.site-footer {
  padding: 1rem;
  text-align: center;
  color: #7890a3;
  font-size: 0.8rem;
}

@media (max-width: 420px) {
  .site-header {
    width: calc(100% - 28px);
  }

  .brand {
    font-size: 1.05rem;
  }

  .site-nav {
    gap: 0.15rem;
  }

  .site-nav a {
    padding: 0.55rem;
    font-size: 0.82rem;
  }
}
</style>