<script>
  import Header from '$lib/Header.svelte';
  import HomeSection from '$lib/HomeSection.svelte';
  import MenuSection from '$lib/MenuSection.svelte';
  import ReservationForm from '$lib/ReservationForm.svelte';
  import AboutSection from '$lib/AboutSection.svelte';

  let activeSection = 'home';
</script>

<Header bind:activeSection />

{#if activeSection == 'home'}
  <HomeSection />
{:else if activeSection == 'menu'}
  <MenuSection />
{:else if activeSection == 'reservation'}
  <ReservationForm />
{:else}
  <AboutSection />
{/if}