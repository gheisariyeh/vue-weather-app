<template>
  <header>
    <nav>
      <RouterLink to="/">Accueil</RouterLink>
      |
      <RouterLink to="/about">À propos</RouterLink>
    </nav>
  </header>

  <main>
    <RouterView />
  </main>
</template>