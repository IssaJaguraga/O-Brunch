<script>
  import { createEventDispatcher } from 'svelte';
  const dispatch = createEventDispatcher();
  
  export let cart = []; 

  let menuItems = [
    {
      id: 1,
      name: "L'Estival",
      price: 19,
      description: "Benedict signature, brioche perdue et granola pistache.",
      badgeType: "Populaire",
      badgeColor: "#E67E5F",
      image: "/images/brunch-estival.jpg"
    },
    {
      id: 2,
      name: "Le Parisien",
      price: 17,
      description: "Gaufres pêches, mini-cupcakes et pancakes au saumon.",
      image: "/images/brunch-parisien.jpg"
    },
    {
      id: 3,
      name: "La Toscane",
      price: 19,
      description: "Pancakes myrtilles, sirop d'érable, saumon et jus frais.",
      badgeType: "Nouveau",
      badgeColor: "#3498DB",
      image: "/images/brunch-toscane.jpg"
    },
    {
      id: 4,
      name: "Le Classique",
      price: 15,
      description: "Œufs pochés, sauce betterave, avocat et bowl passion.",
      image: "/images/brunch-classique.jpg"
    },
    {
      id: 5,
      name: "L'Atlantique",
      price: 17,
      description: "Toast avocat-saumon, œuf poché, smoothie bowl et pancakes.",
      image: "/images/brunch-atlantique.jpg"
    },
    {
      id: 6,
      name: "Le London",
      price: 18,
      description: "Toasts betterave, houmous, avocat sculpté et latte art.",
      badgeType: "Veggie",
      badgeColor: "#27AE60",
      image: "/images/brunch-london.jpg"
    },
    {
      id: 7,
      name: "Le Healthy",
      price: 14,
      description: "Puddings chia aux baies, banana bread et fleur d'avocat.",
      image: "/images/brunch-healthy.jpg"
    },
    {
      id: 8,
      name: "Le Continental",
      price: 16,
      description: "Pancakes chocolat, granola bowl et toast avocat.",
      image: "/images/brunch-continental.jpg"
    },
    {
      id: 9,
      name: "L'Oriental",
      price: 15,
      description: "Poêlée d'œufs, pancakes érable et granola aux figues.",
      image: "/images/brunch-oriental.jpg"
    }
  ];

  $: isInCart = (id) => cart.some(item => item.id === id);

  function handleAdd(item) {
    if (!isInCart(item.id)) {
      dispatch('addToCart', item);
    }
  }

  function goToReservation() {
    dispatch('change', 'reservation');
  }

  function handleRemove(id) {
    dispatch('removeItem', id);
  }
</script>

<section class="menu-container">
  <h2 class="MenuTitle">Notre Menu</h2>
  <p class="MenuSubtitle">Tous nos plats sont faits maison avec des produits frais.</p>

  {#if cart.length > 0}
    <div class="cart-floating-banner">
      <div class="banner-info">
        <span class="cart-icon">🛒</span>
        <span class="cart-count">{cart.length} plat(s) sélectionné(s)</span>
      </div>
      <button class="btn-go-cart" on:click={goToReservation}>
        Voir mon panier →
      </button>
    </div>
  {/if}

  <div class="menu-grid">
    {#each menuItems as item}
      <div class="card">
        {#if item.badgeType}
          <span class="badge" style="background-color: {item.badgeColor}">
            {item.badgeType}
          </span>
        {/if}

        <div class="card-image-container">
          <img src={item.image} alt={item.name} class="card-image" />
        </div>

        <div class="card-content">
          <h3>{item.name}</h3>
          <p class="description">{item.description}</p>

          <div class="bottom">
            <span class="price">{item.price}€</span>

            <div class="button-group">
              {#if isInCart(item.id)}
                <button 
                  class="btn-remove-mini" 
                  on:click={() => handleRemove(item.id)}
                  title="Retirer du panier"
                >
                  ✕
                </button>
                <button class="MenuButton in-cart">
                  Ajouté ! ✓
                </button>
              {:else}
                <button 
                  class="MenuButton" 
                  on:click={() => handleAdd(item)}
                >
                  Commander
                </button>
              {/if}
            </div>
          </div>

          {#if isInCart(item.id)}
            <p class="go-to-res">Prêt à être réservé en bas ! ↓</p>
          {/if}
        </div>
      </div>
    {/each}
  </div>
</section>

<style>
.menu-container {
  padding: 40px 20px 120px 20px;
  text-align: center;
  position: relative;
}

.MenuTitle {
  font-size: 24px;
  color: #2D2424;
  margin-bottom: 15px;
}

.MenuSubtitle { 
  color: #777;
  margin-bottom: 40px; 
  font-style: italic; 
}

/* BANNIÈRE FLOTTANTE */
.cart-floating-banner {
  position: fixed;
  bottom: 30px;
  left: 50%;
  transform: translateX(-50%);
  z-index: 1000;
  background-color: #2D2424;
  color: white;
  padding: 12px 20px;
  border-radius: 50px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 20px;
  width: 90%;
  max-width: 400px;
  box-shadow: 0 10px 30px rgba(0,0,0,0.3);
  animation: slideIn 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275);
}

.banner-info {
  display: flex;
  align-items: center;
  gap: 10px;
}

.cart-count {
  font-weight: 600;
  font-size: 14px;
}

.btn-go-cart {
  background-color: #E67E5F;
  color: white;
  border: none;
  padding: 8px 16px;
  border-radius: 20px;
  font-weight: bold;
  font-size: 13px;
  cursor: pointer;
}

@keyframes slideIn {
  from { transform: translate(-50%, 100px); opacity: 0; }
  to { transform: translate(-50%, 0); opacity: 1; }
}

.menu-grid {
  max-width: 1200px;
  margin: auto;
  display: grid;
  grid-template-columns: 1fr;
  gap: 20px;
}

@media (min-width: 768px) {
  .menu-grid {
    grid-template-columns: repeat(3, 1fr);
  }
}

.card {
  background: #fff;
  border-radius: 15px;
  box-shadow: 0 5px 15px rgba(0,0,0,0.15);
  position: relative;
  overflow: hidden;
  text-align: left;
  display: flex;
  flex-direction: column;
  transition: transform 0.3s ease;
}

.card:hover {
  transform: translateY(-5px);
}

.badge {
  position: absolute;
  top: 10px;
  right: 10px;
  color: white;
  padding: 4px 10px;
  font-size: 12px;
  border-radius: 12px;
  z-index: 2;
}

.card-image-container {
  width: 100%;
  overflow: hidden;
  aspect-ratio: 1 / 1;
}

.card-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.card-content {
  padding: 15px;
  display: flex;
  flex-direction: column;
  flex-grow: 1;
}

h3 {
  margin-bottom: .5rem;
  color: #2D2424;
  font-size: 17px;
}

.description {
  color: #4A3F3F;
  font-size: 14px;
  margin-bottom: 15px;
}

.bottom {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-top: auto;
}

.price {
  font-weight: bold;
  font-size: 18px;
  color: #E67E5F;
}

button.MenuButton {
  background-color: #2D2424;
  color: white;
  border: none;
  padding: 10px 20px;
  border-radius: 25px;
  cursor: pointer;
  font-weight: 600;
  transition: all 0.2s ease;
}

button.MenuButton:hover:not(.in-cart) {
  background-color: #E67E5F;
  transform: scale(1.05);
}

button.in-cart {
  background-color: #27AE60;
  cursor: default;
}
.button-group {
  display: flex;
  align-items: center;
  gap: 8px;
}

.btn-remove-mini {
  background-color: #ffeded;
  color: #e74c3c;
  border: 1px solid #e74c3c;
  width: 32px;
  height: 32px;
  border-radius: 50%;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  font-weight: bold;
  transition: all 0.2s;
}

.btn-remove-mini:hover {
  background-color: #e74c3c;
  color: white;
}

.go-to-res {
  font-size: 11px;
  color: #27AE60;
  margin-top: 8px;
  font-weight: bold;
  text-align: right;
  animation: fadeIn 0.5s ease-in;
}

@keyframes fadeIn {
  from { opacity: 0; transform: translateY(-5px); }
  to { opacity: 1; transform: translateY(0); }
}
</style>