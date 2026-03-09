<script>
  import { createEventDispatcher } from 'svelte';
  const dispatch = createEventDispatcher();

let menuItems = [
    {
      id: 1,
      name: "L'Estival",
      price: 19,
      description: "Benedict signature, brioche perdue et granola pistache.",
      badgeType: "Populaire",
      badgeColor: "#E67E5F",
      image: "/images/brunch-estival.jpg.jpg"
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
      image: "/images/brunch-toscane.jpg.jpg"
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

  function handleAdd(item) {
    dispatch('addToCart', item); // envoie le brunch au parent
  }
</script>

<section class="menu-container">
  <h2 class="MenuTitle">Notre Menu</h2>
  <p class="MenuSubtitle">Tous nos plats sont faits maison avec des produits frais.</p>

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
            <button class="MenuButton" on:click={() => handleAdd(item)}>Commander</button>
          </div>
        </div>

      </div>
    {/each}
  </div>
</section>

<style>

/* ----- SECTION MENU ----- */
.menu-container {
  padding: 40px 20px;
  text-align: center;
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

.menu-grid {
  max-width: 1200px;
  margin: auto;
  display: grid;
  grid-template-columns: 1fr;
  gap: 15px;
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
  transform: translateY(-5px); /* La carte se soulève un peu */
}

/* Badge */
.badge {
  position: absolute;
  top: 10px;
  right: 10px;
  color: white;
  padding: 4px 10px;
  font-size: 12px;
  border-radius: 12px;

}

/* Image container */
.card-image-container {
  width: 100%;
  overflow: hidden;
  aspect-ratio: 1 / 1; /* force un carré */
}

.card-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
  object-position: center; 
}

/* Content */
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

button {
  background-color: #2D2424;
  color: white;
  border: none;
  padding: 10px 20px;
  border-radius: 25px;
  cursor: pointer;
  font-weight: 600;
  transition: all 0.2s ease;
}

button:hover {
  background-color: #E67E5F; /* Change de couleur au survol */
  transform: scale(1.05);
  opacity: 0.9;
}

button:active {
  transform: scale(0.95); /* Effet de pression quand on clique */
}
</style>