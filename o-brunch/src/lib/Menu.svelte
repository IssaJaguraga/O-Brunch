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
   <button
        class:selected={activeSection === 'home'} 
        on:click={() => changeSection ('home')}>
        Accueil
    </button>

    <button 
        class:selected={activeSection === 'menu'} 
        on:click={() => changeSection ('menu')}>
        Menu
    </button>

    <button 
        class:selected={activeSection === 'reservation'} 
        on:click={() => changeSection ('reservation')}>
        Réservation
    </button>

    <button 
        class:selected={activeSection === 'about'} 
        on:click={() => changeSection ('about')}>
        À propos
    </button>
</nav>


<style>
  nav {
    display: none;
    flex-direction: column;
    margin-top: 16px;
    gap: 12px;
    padding-bottom: 10px; /* Ajoute un peu d'espace en bas */
  }

  nav.open {
    display: flex;
  }

  button {
    background: none;
    border: none;
    font-size: 20px;
    cursor: pointer;
    color: #2D2424;
    transition: color 0.3s ease;
    padding: 8px 0;
  }

  .selected {
    font-weight: bold;
    color: #E67E5F;
  }
  
  button:hover {
    color: #E67E5F; /* Interactif au survol */
  }

  /* Desktop */
  @media (min-width: 1024px) {
    nav {
      display: flex;
      flex-direction: row;
      justify-content: center;
      gap: 2rem;
      margin-top: 16px;
    }
  }
</style>