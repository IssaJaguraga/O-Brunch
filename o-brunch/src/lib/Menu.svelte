<script>
  import { createEventDispatcher } from 'svelte';
  export let isMenuOpen;
  export let activeSection;

  const dispatch = createEventDispatcher();

  function changeSection(section) {
    dispatch('change', section);
    isMenuOpen = false;
  }
</script>

<nav class:open={isMenuOpen}>
  <button class:selected={activeSection === 'home'} 
  on:click={() => changeSection('home')}>Accueil
  </button>

  <button class:selected={activeSection === 'menu'} 
  on:click={() => changeSection('menu')}>Menu
  </button>

  <button class:selected={activeSection === 'reservation'} 
  on:click={() => changeSection('reservation')}>Réservation
  </button>

  <button class:selected={activeSection === 'about'} 
  on:click={() => changeSection('about')}>À propos
  </button>
</nav>

<style>
  nav {
    display: none; 
    flex-direction: column;
    align-items: center; 
    justify-content: center; 
    gap: 15px;
    width: 100%;
    padding-bottom: 35px; 
  }

  nav.open {
    display: flex; /* S'affiche quand on clique */
  }

  button {
    background: none;
    border: none;
    font-size: 20px;
    color: #2D2424;
    cursor: pointer;
    width: fit-content; /* Le bouton prend juste la place de son texte */
  }

  button:hover {
    color: #E67E5F; /* Le bouton change de couleur au survol */
  }

  .selected {
    font-weight: bold;
    color: #E67E5F;
  }

  @media (max-width: 600px) {
    nav {
      /* On augmente la marge pour laisser passer le logo qui dépasse */
      margin-top: 55px; 
      width: 100%;
    }
  }

  @media (min-width: 1024px) {
    nav {
      display: flex;
      flex-direction: row;
      justify-content: center;
      margin-top: 15px;
      gap: 30px;
    }
  }
</style>