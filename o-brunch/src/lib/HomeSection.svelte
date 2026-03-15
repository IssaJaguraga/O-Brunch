<script>
  import { createEventDispatcher } from "svelte";
  
  const dispatch = createEventDispatcher();

  export let cart = [];

  function goToMenu() {
    dispatch('change', 'menu');
  }

  function goToReservation() {
    dispatch('change', cart.length > 0 ? 'reservation' : 'menu');
  }

  const features = [
    {
      title: "Fraîcheur",
      text: "Produits de saison et pain artisanal."
    },
    {
      title: "Fait Maison",
      text: "Recettes préparées avec amour chaque matin."
    },
    {
      title: "Ambiance cosy",
      text: "Un lieu chaleureux pour partager un moment unique."
    },
    {
      title: "Ouvert 7j/7",
      text: "De 8h à 16h non-stop."
    }
  ];
</script>

<section class="home">
  <div class="home-content">
    <h1>Bienvenue chez O'Brunch ☕🥞</h1>
    
    <p class="home-text-highlight">
      Oubliez le petit-déjeuner classique. Nous avons réinventé l'art du brunch pour en faire un rendez-vous quotidien.
    </p>
    
    <p>Venez déguster nos brunchs maison, frais et savoureux, tous les jours de la semaine !</p>
    
    <p class="story">
      Plus qu'un repas, une parenthèse gourmande. Chez <strong>O'Brunch</strong>, nous transformons vos matinées en moments d'exception.
    </p>

    <div class="cta">
      <button on:click={goToMenu}>
        Voir le menu
      </button>
      
      <button class="secondary" on:click={goToReservation}>
        {#if cart.length > 0}
          Finaliser ma commande ({cart.length})
        {:else}
          Réserver une table
        {/if}
      </button>
    </div>
  </div>

  <div class="features">
    {#each features as feature}
      <div class="feature-item">
        <h3>{feature.title}</h3>
        <p>{feature.text}</p>
      </div>
    {/each}
  </div>

  <div class="home-image">
    <img src="/images/img_home.jpg" alt="Table garnie avec pancakes, fruits et café chez O'Brunch" />
  </div>
</section>

<style>
  .home-image {
    max-width: 750px; /* limite la largeur sur grands écrans */
    margin: 30px auto 0; /* centre et espace du haut */
    /* garde un joli arrondi */
    overflow: hidden; /* arrondi propre */
  }

  .home-image img {
    width: 100%;
    height: auto;
    display: block;
    object-fit: cover; /* garde le ratio et découpe si besoin */
  }
  
  .home {
    text-align: center;
  }

  .home-content {
    padding: 0 20px;
  }

  h1 {
    font-size: 23px;
    font-weight: 800;
    color: #2D2424;
    margin: 40px 0 20px;
  }

  p {
    font-size: 17px;
    line-height: 1.6;
    color: #4A3F3F;
    margin-bottom: 20px;
  }

  .home-text-highlight {
    font-weight: 700;
    color: #E67E5F;
  }

  .story {
    font-style: italic;
    border-top: 1px solid #eee;
    padding-top: 20px;
  }

  /* Boutons */
  .cta {
    margin: 30px 0;
    display: flex;
    justify-content: center;
    gap: 15px;
    flex-wrap: wrap;
  }

  .cta button {
    background-color: #E67E5F;
    color: white;
    border: none;
    padding: 12px 25px;
    border-radius: 25px;
    font-size: 16px;
    cursor: pointer;
  }

  .cta button:hover {
    opacity: 0.9;
  }

  .cta .secondary {
    background-color: #2D2424;
  }

  .features {
    display: grid;
    grid-template-columns: 1fr;
    gap: 20px;
    margin: 40px 20px;
    padding: 20px;
    background: #fdfaf8;
    border-radius: 15px;
  }

  .feature-item {
    border-bottom: 1px solid #eee; /* Séparateur sur mobile */
  }

  /* On enlève la bordure sur le dernier item */
  .feature-item:last-child {
    border-bottom: none;
  }

  .feature-item h3 {
    font-size: 18px;
    color: #E67E5F; /* Utilise ta couleur dominante pour les titres */
    margin-bottom: 5px;
  }

  .feature-item p {
    font-size: 14px;
    margin-bottom: 0;
  }

  /* VERSION DESKTOP (Tablette et ordi) */
  @media (min-width: 768px) {
    .features {
      grid-template-columns: repeat(4, 1fr); /* 4 colonnes alignées */
      gap: 10px;
    }

    .feature-item {
      border-bottom: none;
      border-right: 1px solid #eee; /* Séparateur vertical entre les items */
    }

    .feature-item:last-child {
      border-right: none;
    }
  }
</style>