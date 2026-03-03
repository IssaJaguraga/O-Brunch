<script>
  import Header from '$lib/Header.svelte';
  import HomeSection from '$lib/HomeSection.svelte';
  import MenuSection from '$lib/MenuSection.svelte';
  import ReservationForm from '$lib/ReservationForm.svelte';
  import AboutSection from '$lib/AboutSection.svelte';

  let activeSection = 'home';

  function changeSection(event) {
    activeSection = event.detail;
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
    <MenuSection />
  {:else if activeSection === 'reservation'}
    <ReservationForm />
  {:else}
    <AboutSection />
  {/if}
</main>