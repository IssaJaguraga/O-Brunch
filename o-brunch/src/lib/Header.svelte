<script>
  import { createEventDispatcher } from 'svelte';
  import Menu from './Menu.svelte';

  export let activeSection;
  const dispatch = createEventDispatcher();
  let isMenuOpen = false;

  function changeSection(section) {
    dispatch('change', section);
    isMenuOpen = false; // ferme le menu quand on clique sur une section
  }

  function toggleMenu() {
    isMenuOpen = !isMenuOpen;
  }

  function goHome() {
    dispatch("change", "home");
  }
</script>

<header class="header-container">

  <div class="header-navigation">
    <button class="header-logo" on:click={goHome}>
      <img src="/images/logo.png" alt="Logo O'Brunch" />
    </button>

    <button class="burger-button" on:click={toggleMenu}>
      <img src="/images/menu_icon_burger.png" alt="Menu" />
    </button>
  </div>

  <Menu bind:isMenuOpen {activeSection} on:change={(e) => changeSection(e.detail)} />

</header>

<style>
  .header-container {
    background-color: rgba(255, 255, 255, 0.8);
    position: sticky;
    top: 0;
    z-index: 1000;
    padding: 0 16px; 
    margin-bottom: 50px;
  }

  .header-navigation {
    display: flex;
    justify-content: space-between;
    align-items: center;
    max-width: 1200px;
    margin: 0 auto;
    height: 45px;
  }

  .header-logo {
    background-color: #fbe9e4;
    border-radius: 30px;
    padding: 10px 30px ;
    position: relative;
    top: 18px; 
    border: 2px solid #F2A38A;
    cursor: pointer;
  }

  .header-logo img {
    height: 35px;
    display: block; 
  }

  .burger-button {
    background: none;
    border: none;
    cursor: pointer;
  }

  .burger-button img {
    width: 47px;
    margin-top: 40px;
    border-radius: 7px;
  }

  @media (min-width: 1024px) {
    .burger-button { 
      display: none; 
    }
    .header-logo {
      margin: 40px 0 2px;
    }
  }
</style>