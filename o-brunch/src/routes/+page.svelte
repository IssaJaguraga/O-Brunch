<script>
  import Header from '$lib/Header.svelte';
  import HomeSection from '$lib/HomeSection.svelte';
  import MenuSection from '$lib/MenuSection.svelte';
  import ReservationForm from '$lib/ReservationForm.svelte';
  import AboutSection from '$lib/AboutSection.svelte';

  let activeSection = 'home';

  // Panier pour stocker les brunchs choisis
  let cart = [];

  function changeSection(event) {
    activeSection = event.detail;
  }

  // Ajouter un brunch au panier
  function addToCart(item) {
    cart = [...cart, item];
    alert(`${item.name} ajouté au panier !`);
  }

  // Soumettre la réservation avec le panier
  function submitReservation(reservationData) {
    alert(
      `Merci ${reservationData.name}, votre réservation pour ${reservationData.guests} personne(s) le ${reservationData.date} est confirmée !\n\n` +
      `Vous avez réservé :\n` + cart.map(i => `- ${i.name} (${i.price}€)`).join("\n")
    );
    cart = []; // réinitialiser le panier après réservation
  }
</script>

<Header
  {activeSection}
  on:change={changeSection}
/>

<main class="container">
  {#if activeSection === 'home'}
    <HomeSection on:change={changeSection} />
  {:else if activeSection === 'menu'}
    <MenuSection on:addToCart={addToCart} />
  {:else if activeSection === 'reservation'}
    <ReservationForm {cart} on:submitReservation={submitReservation} />
  {:else}
    <AboutSection />
  {/if}
</main>
