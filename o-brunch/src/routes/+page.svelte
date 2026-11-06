<script>
  import Header from '#lib/Header.svelte';
  import HomeSection from '#lib/HomeSection.svelte';
  import MenuSection from '#lib/MenuSection.svelte';
  import ReservationForm from '#lib/ReservationForm.svelte';
  import AboutSection from '#lib/AboutSection.svelte';

  let activeSection = 'home';
  let cart = [];
  let confirmationMessage = '';
  let menuOpen = false; // <-- ajout de l'état du menu mobile

  function changeSection(event) {
    activeSection = event.detail;
    menuOpen = false; // ferme le menu quand on change de section
  }

  function addToCart(event) {
    const item = event.detail;
    const exists = cart.some(i => i.id === item.id);
    if (!exists) {
      cart = [...cart, { ...item, quantity: 1 }];
    }
  }

  function handleRemoveItem(event) {
    const id = event.detail;
    cart = cart.filter(item => item.id !== id);
  }

  function submitReservation(event) {
    const reservationData = event.detail;
    confirmationMessage = `Merci ${reservationData.name}, votre réservation pour ${reservationData.guests} personne(s) le ${reservationData.date} à ${reservationData.time} est confirmée ! Total : ${reservationData.total}€`;
    cart = []; 
    activeSection = 'home';
    menuOpen = false; // ferme le menu si ouvert
  }
</script>

<Header 
  {activeSection} 
  bind:isMenuOpen={menuOpen} 
  on:change={changeSection} 
/>

{#if confirmationMessage}
  <div class="confirmation-banner">
    {confirmationMessage}
    <button class="close-btn" on:click={() => confirmationMessage = ''}>✕</button>
  </div>
{/if}

<main class="container">
  {#if activeSection === 'home'}
    <HomeSection {cart} on:change={changeSection} />
  
  {:else if activeSection === 'menu'}
    <MenuSection 
      {cart} 
      on:addToCart={addToCart} 
      on:removeItem={handleRemoveItem}
      on:change={changeSection} 
    />
  
  {:else if activeSection === 'reservation'}
    <ReservationForm 
      {cart} 
      on:removeItem={handleRemoveItem}
      on:submitReservation={submitReservation} 
    />
  
  {:else if activeSection === 'about'}
    <AboutSection />
  {/if}
</main>

<style>
  .confirmation-banner {
    position: fixed;
    top: 20px;
    left: 50%;
    transform: translateX(-50%);
    background-color: #27AE60;
    color: white;
    padding: 15px 25px;
    border-radius: 10px;
    box-shadow: 0 5px 20px rgba(0,0,0,0.2);
    z-index: 1000;
    display: flex;
    align-items: center;
    gap: 15px;
    max-width: 90%;
    font-weight: bold;
  }

  .close-btn {
    background: none;
    border: none;
    color: white;
    font-size: 16px;
    cursor: pointer;
  }
</style>