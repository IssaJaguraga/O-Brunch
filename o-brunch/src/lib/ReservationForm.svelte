<script>
  import { createEventDispatcher } from 'svelte';

  export let cart = []; // reçoit le panier depuis +page.svelte
  const dispatch = createEventDispatcher();

  let name = "";
  let date = "";
  let guests = 1;

  const submitForm = () => {
    if (cart.length === 0) {
      alert("Votre panier est vide ! Veuillez ajouter au moins un brunch avant de réserver.");
      return;
    }

    // on envoie les données au parent
    dispatch('submitReservation', {
      name,
      date,
      guests,
      cart
    });

    // réinitialisation du formulaire
    name = "";
    date = "";
    guests = 1;
  };

  // optionnel : supprimer un item du panier avant de réserver
  function removeFromCart(index) {
    cart = cart.filter((_, i) => i !== index);
  }
</script>

<section class="reservation">
  <h2>Réserver une table</h2>

  {#if cart.length > 0}
    <div class="cart-preview">
      <h3>Votre panier :</h3>
      <ul>
        {#each cart as item, i}
          <li>
            {item.name} ({item.price}€)
            <button type="button" on:click={() => removeFromCart(i)}>Supprimer</button>
          </li>
        {/each}
      </ul>
    </div>
  {/if}

  <form on:submit|preventDefault={submitForm}>
    <input type="text" placeholder="Votre nom" bind:value={name} required />
    <input type="date" bind:value={date} required />
    <input type="number" min="1" placeholder="Nombre de personnes" bind:value={guests} required />
    <button type="submit">Réserver</button>
  </form>
</section>

<style>
  .reservation {
    margin: 2rem;
    text-align: center;
  }

  form {
    display: flex;
    flex-direction: column;
    gap: 1rem;
    max-width: 400px;
    margin: auto;
  }

  input, button {
    padding: 0.5rem;
    font-size: 1rem;
  }

  button {
    background-color: #c59d5f;
    color: white;
    border: none;
    cursor: pointer;
    border-radius: 6px;
  }

  button:hover {
    background-color: #a17845;
  }

  .cart-preview {
    background: #f9f2e7;
    padding: 1rem;
    border-radius: 10px;
    margin-bottom: 1.5rem;
    text-align: left;
  }

  .cart-preview ul {
    list-style: none;
    padding: 0;
  }

  .cart-preview li {
    display: flex;
    justify-content: space-between;
    margin-bottom: 0.5rem;
  }

  .cart-preview button {
    background-color: #e67e5f;
    padding: 2px 6px;
    font-size: 0.8rem;
  }

  .cart-preview button:hover {
    background-color: #d0563f;
  }
</style>