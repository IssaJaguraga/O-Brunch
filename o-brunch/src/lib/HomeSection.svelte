<script>
</script>

<section class="home">
  <div class="content-wrapper">
    <h1>Bienvenue chez O'Brunch ☕🥞</h1>
    
    <p class="highlight">Oubliez le petit-déjeuner classique. Nous avons réinventé l'art du brunch pour en faire un rendez-vous quotidien.</p>
    
    <p>Venez déguster nos brunchs maison, frais et savoureux, tous les jours de la semaine !</p>
    
    <p>Une cuisine authentique où chaque produit est sélectionné avec soin pour réveiller vos papilles.</p>
    
    <p class="story">
      Plus qu'un repas, une parenthèse gourmande. Chez <strong>O'Brunch</strong>, nous transformons vos matinées en moments d'exception avec des recettes généreuses et des produits frais.
    </p>

    <div class="features">
      <div class="feature-item">
        <h3>Fraîcheur</h3>
        <p>Produits de saison et pain artisanal.</p>
      </div>

      <div class="feature-item">
        <h3>Fait Maison</h3>
        <p>Recettes préparées avec amour chaque matin.</p>
      </div>
    </div>
  </div>

  <img src="/images/img_home.jpg" alt="Table garnie O'Brunch" />
</section>

<style>
  .home {
    text-align: center;
    width: 100%;
  }

  .content-wrapper {
    padding: 0 20px; /* Évite que le texte touche les bords */
  }

  .home h1 {
    font-size: 23px;
    margin-bottom: 24px;
    margin-top: 20px;
    font-weight: 800;
    color: #2D2424;
  }

  .home p {
    font-size: 17px;
    margin-bottom: 20px;
    line-height: 1.6;
    color: #4A3F3F;
  }

  .highlight {
    font-weight: 700;
    color: #E67E5F; /* Couleur Terracotta pour la phrase d'accroche */
  }

  .story {
    font-style: italic;
    border-top: 1px solid rgba(0,0,0,0.05);
    padding-top: 20px;
    margin-top: 20px;
  }

  .features {
    display: flex;
    flex-direction: column;
    gap: 20px;
    margin: 30px 0;
  }

  .home h3 {
    font-size: 18px;
    color: #2D2424;
    margin-bottom: 5px;
  }

  .home img {
    width: 100%;
    display: block;
    height: auto;
    margin-top: 24px;
    border-radius: 0 0 20px 20px;
  }

  /* Tablette et Desktop */
  @media (min-width: 768px) {
    .home h1 { font-size: 32px; }
    .home p { font-size: 19px; }
    
    .features {
      flex-direction: row;
      justify-content: center;
      gap: 60px;
    }
  }

  @media (min-width: 1024px) {
    .home h1 { font-size: 45px; }
    .home p { font-size: 21px; }
  }
</style>