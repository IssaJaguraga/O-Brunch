

<script>
  let menuItems = [
    { id: 1, name: "Brunch Classique", price: 15, description: "Œufs, bacon, pancakes, jus d'orange" },
    { id: 2, name: "Brunch Veggie", price: 14, description: "Avocat, œufs, pain complet, smoothie" },
    { id: 3, name: "Brunch Deluxe", price: 20, description: "Tout ce qu'il y a de meilleur avec boisson chaude" },
  ];
</script>

<section class="menu">
  <h2>Notre Menu</h2>
  <ul>
    {#each menuItems as item}
      <li>
        <h3>{item.name} - {item.price}€</h3>
        <p>{item.description}</p>
      </li>
    {/each}
  </ul>
</section>

<style>
  .menu {
    margin: 2rem;
  }
  .menu ul {
    list-style: none;
    padding: 0;
  }
  .menu li {
    margin-bottom: 1.5rem;
    border-bottom: 1px solid #ddd;
    padding-bottom: 0.5rem;
  }
</style>