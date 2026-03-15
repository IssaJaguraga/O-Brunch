<script>
  import { createEventDispatcher } from 'svelte';
  import { slide } from 'svelte/transition';
  export let isMenuOpen;
  export let activeSection;

  const dispatch = createEventDispatcher();

  const sections = [
    { id: 'home', label: 'Accueil' },
    { id: 'menu', label: 'Menu' },
    { id: 'reservation', label: 'Réservation' },
    { id: 'about', label: 'À propos' }
  ];

  function changeSection(sectionId) {
    dispatch('change', sectionId);
    dispatch('closeMenu'); // informe le parent de fermer le menu
  }
</script>

<nav class:open={isMenuOpen}>
  {#each sections as section}
    <button
      class:selected={activeSection === section.id}
      on:click={() => changeSection(section.id)}
      aria-current={activeSection === section.id ? 'page' : undefined}>
      {section.label}
    </button>
  {/each}
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
    display: flex;
  }

  button {
    background: none;
    border: none;
    font-size: 20px;
    color: #2D2424;
    cursor: pointer;
    width: fit-content;
  }

  button:hover {
    color: #E67E5F;
  }

  .selected {
    font-weight: bold;
    color: #E67E5F;
  }

  @media (max-width: 600px) {
    nav {
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