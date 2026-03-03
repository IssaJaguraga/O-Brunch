<script>
  import { createEventDispatcher } from "svelte";
  
  const dispatch = createEventDispatcher();

  function goToMenu() {
    dispatch("change", "menu");
  }

  function goToReservation() {
    dispatch("change", "reservation");
  }
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
      <button on:click={goToMenu}>Voir le menu</button>
      <button class="secondary" on:click={goToReservation}>Réserver</button>
    </div>

    <div class="features">
      <div class="feature-item">
        <h3>Fraîcheur</h3>
        <p>Produits de saison et pain artisanal.</p>
      </div>
      <div class="feature-item">
        <h3>Fait Maison</h3>
        <p>Recettes préparées avec amour chaque matin.</p>
      </div>

      <div class="feature-item">
        <h3>Ambiance cosy</h3>
        <p>Un lieu chaleureux pour partager un moment unique.</p>
      </div>

      <div class="feature-item">
        <h3>Ouvert 7j/7</h3>
        <p>De 8h à 16h non-stop.</p>
      </div>
    </div>
  </div>

  <img src="/images/img_home.jpg" alt="Table garnie avec pancakes, fruits et café chez O'Brunch" />
</section>

<style>
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
    display: flex;
    flex-direction: column;
    margin: 30px 0;
  }

  .feature-item h3 {
    font-size: 18px;
    gap: 20px;
    color: #2D2424;
  }

  img {
    width: 100%;
    border-radius: 0 0 20px 20px;
    display: block;
  }

  @media (min-width: 768px) {
    .features {
      flex-direction: row;
      justify-content: center;
    }
  }
</style>