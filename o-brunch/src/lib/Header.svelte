<script>
  import { createEventDispatcher } from 'svelte';
  import Menu from './Menu.svelte';

  export let activeSection;
  const dispatch = createEventDispatcher();

  let isMenuOpen = false;

  function changeSection(section) {
    dispatch('change', section);
  }

  function toggleMenu() {
    isMenuOpen = !isMenuOpen;
  }
</script>

<header class="header">
  <div class="top-bar">
    <a href="/" class="logo">
      <img src="/images/logo.png" alt="Logo O'Brunch">
    </a>

    <button 
      class="burger" 
      on:click={toggleMenu}
      aria-label="Ouvrir le menu">
      <img src="/images/menu_icon_burger.png" alt="Menu" />
    </button>
  </div>

  <Menu
    bind:isMenuOpen
    {activeSection}
    on:change={(e) => changeSection(e.detail)}
  />
</header>

<style>
 .header {
  background: rgba(255, 255, 255, 0.7); 
  padding: 16px;
  position: sticky; /* Le header reste en haut au scroll */
  top: 0;
  z-index: 1000;
 
  }

  .top-bar {
    display: flex;
    justify-content: space-between;
    align-items: center;
    max-width: 1200px;
    margin: 0 auto; /* Aligné avec ton container */
  }
  .logo img 
  {
    height: 45px;
    display: block;
  }

  .burger {
    background: none;
    border: none;
    cursor: pointer;
    padding: 0;
  }

 .burger img 
 {
    width: 28px;
    height: auto;
    border-radius: 3px;
  }

  /* Desktop */
  @media (min-width: 1024px) 
  {
    .burger {
      display: none;
    }
  }
</style>