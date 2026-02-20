<script>
    export let activeSection; // on reçoit la variable depuis +page.svelte
</script>

<nav>
    <button 
      class:selected={activeSection === 'home'} 
      on:click={() => activeSection = 'home'}>
      Accueil
    </button>

    <button 
      class:selected={activeSection === 'menu'} 
      on:click={() => activeSection = 'menu'}>
      Menu
    </button>

    <button 
      class:selected={activeSection === 'reservation'} 
      on:click={() => activeSection = 'reservation'}>
      Réservation
    </button>

    <button 
      class:selected={activeSection === 'about'} 
      on:click={() => activeSection = 'about'}>
      À propos
    </button>
</nav>


<style>
  nav {
    display: flex;
    gap: 1rem;
    background-color: #f5f5f5;
    padding: 1rem;
  }

  button {
    background: none;
    border: none;
    font-size: 1rem;
    cursor: pointer;
  }

  .selected {
    font-weight: bold;
    color: #c59d5f;
  }
</style>