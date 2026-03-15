<script>
  import { createEventDispatcher } from 'svelte';

  export let cart = []; // Reçoit le panier depuis +page.svelte
  const dispatch = createEventDispatcher();

  let name = "";
  let date = "";
  let time = "";
  let guests = 1;

  // Générer les créneaux horaires de 08:00 à 15:30
  const timeSlots = [
    "08:00", "08:30", "09:00", "09:30", "10:00", "10:30", 
    "11:00", "11:30", "12:00", "12:30", "13:00", "13:30", 
    "14:00", "14:30", "15:00", "15:30"
  ];

  // Calcul du total dynamique
  $: total = cart.reduce((sum, item) => sum + (item.price * (item.quantity || 1)), 0);

  const submitForm = () => {
    dispatch('submitReservation', {
      name,
      date,
      time,
      guests,
      cart,
      total
    });

    // Reset du formulaire
    name = "";
    date = "";
    time = "";
    guests = 1;
  };

  function removeFromCart(id) {
    // Envoie l'ID au parent pour suppression réelle dans le store/panier
    dispatch('removeItem', id);
  }
</script>

<section class="reservation-container">
  <div class="reservation-card">
    <h2 class="title">Finaliser ma réservation</h2>
    <p class="subtitle">Réservez votre table et pré-commandez vos brunchs préférés.</p>

    <div class="cart-section">
      <h3>🛒 Récapitulatif de ma commande</h3>
      
      {#if cart.length > 0}
        <ul class="cart-list">
          {#each cart as item (item.id)}
            <li class="cart-item">
              <div class="item-info">
                <span class="item-name">{item.name}</span>
                <span class="item-price">{item.price}€</span>
              </div>
              <button 
                type="button" 
                class="btn-remove" 
                on:click={() => removeFromCart(item.id)}
                aria-label="Supprimer {item.name}"
              >
                &times;
              </button>
            </li>
          {/each}
        </ul>

        <div class="total-bar">
          <span>Total à régler sur place :</span>
          <span class="total-amount">{total}€</span>
        </div>
      {:else}
        <p class="empty-msg">Votre panier est vide... pour l'instant ! ✨</p>
      {/if}
    </div>

    <hr class="separator" />

    <form on:submit|preventDefault={submitForm} class="res-form">

      <div class="input-group">
        <label for="name">Nom</label>
        <input
          id="name"
          type="text"
          placeholder="Ex: Jean Dupont"
          bind:value={name}
          required
        />
      </div>

      <div class="form-row">

        <div class="input-group">
          <label for="date">Date</label>
          <input
            id="date"
            type="date"
            bind:value={date}
            required
          />
        </div>

        <div class="input-group">
          <label for="time">Heure</label>
          <select
            id="time"
            bind:value={time}
            required
          >
            <option value="" disabled selected>Choisir une heure</option>
            {#each timeSlots as slot}
              <option value={slot}>{slot}</option>
            {/each}
          </select>
        </div>

        <div class="input-group">
          <label for="guests">Personnes</label>
          <input
            id="guests"
            type="number"
            min="1"
            max="10"
            bind:value={guests}
            required
          />
        </div>

      </div>

      <button
        type="submit"
        class="btn-submit"
        disabled={cart.length === 0}
      >
        Confirmer ma réservation
      </button>

    </form>
  </div>
</section>

<style>
  .reservation-container {
    padding: 60px 20px;
    display: flex;
    justify-content: center;
    font-family: sans-serif; /* Assure une base propre */
  }

  .reservation-card {
    width: 100%;
    max-width: 500px;
    padding: 30px;
    border-radius: 20px;
    box-shadow: 0 15px 35px rgba(0,0,0,0.1);
    background: white;
  }

  .title {
    font-size: 24px;
    color: #2D2424;
    margin-bottom: 5px;
    text-align: center;
  }

  .subtitle {
    color: #888;
    font-size: 14px;
    margin-bottom: 30px;
    text-align: center;
  }

  .cart-section {
    background: #fcf8f4;
    padding: 20px;
    border-radius: 15px;
    margin-bottom: 25px;
  }

  .cart-section h3 {
    font-size: 16px;
    margin-bottom: 15px;
    color: #4A3F3F;
  }

  .cart-list {
    list-style: none;
    padding: 0;
    margin: 0;
  }

  .cart-item {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 12px 0;
    border-bottom: 1px solid #eee;
  }

  .item-info {
    display: flex;
    flex-direction: column;
  }

  .item-name {
    font-weight: 600;
    color: #2D2424;
  }

  .item-price {
    font-size: 13px;
    color: #E67E5F;
  }

  /* Style de la croix de suppression */
  .btn-remove {
    background: none;
    border: none;
    color: #bbb;
    font-size: 24px;
    font-weight: 300;
    cursor: pointer;
    line-height: 1;
    padding: 5px 10px;
    transition: all 0.2s ease;
  }

  .btn-remove:hover {
    color: #ff4d4d;
    transform: scale(1.2);
  }

  .total-bar {
    margin-top: 15px;
    display: flex;
    justify-content: space-between;
    font-weight: 800;
    font-size: 18px;
    color: #2D2424;
  }

  .total-amount {
    color: #E67E5F;
  }

  .separator {
    border: 0;
    border-top: 1px solid #eee;
    margin: 25px 0;
  }

  .res-form {
    display: flex;
    flex-direction: column;
    gap: 15px;
  }

  .input-group {
    display: flex;
    flex-direction: column;
    gap: 5px;
    text-align: left;
  }

  .input-group label {
    font-size: 12px;
    font-weight: bold;
    text-transform: uppercase;
    color: #888;
  }

  .form-row {
    display: grid;
    grid-template-columns: 1fr 1fr 0.8fr; /* Ajusté pour 3 colonnes */
    gap: 15px;
  }

  input, select {
    padding: 12px;
    border: 1px solid #ddd;
    border-radius: 10px;
    font-size: 15px;
    transition: border 0.3s;
  }

  input:focus, select:focus {
    outline: none;
    border-color: #E67E5F;
  }

  .btn-submit {
    margin-top: 10px;
    background-color: #2D2424;
    color: white;
    border: none;
    padding: 15px;
    border-radius: 30px;
    font-weight: bold;
    font-size: 16px;
    cursor: pointer;
    transition: 0.3s;
  }

  .btn-submit:hover:not(:disabled) {
    background-color: #E67E5F;
    transform: translateY(-2px);
  }

  .btn-submit:disabled {
    background-color: #ccc;
    cursor: not-allowed;
  }

  .empty-msg {
    font-style: italic;
    color: #999;
    text-align: center;
    padding: 10px;
  }
</style>