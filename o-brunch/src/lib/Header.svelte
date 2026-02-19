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