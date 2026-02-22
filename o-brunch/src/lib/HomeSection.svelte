

<script>
  // tu peux ajouter des images ou infos du restaurant
</script>

<section class="home">
  <h1>Bienvenue chez O'Brunch ☕🥞</h1>
  <p>Venez déguster nos brunchs maison, frais et savoureux, tous les jours de la semaine !</p>
  
  <img src="/images/img_home.jpg" alt="Brunch O'Brunch" />
</section>

<style>
  .home 
  {
  text-align: center;
  margin: 0 auto;
  padding: 24px 0;
  }

  .home h1 
  {
  font-size: 23px;
  margin-bottom: 16px;
  }

  .home p 
  {
  font-size: 16px;
  margin-bottom: 18px;
  }

  .home img 
  {
  width: 100%;
  max-width: 400px;
  border-radius: 10px;
  margin-top: 16px;
  }


/* Tablette */
@media (min-width: 768px)
{
  .home h1 
  { font-size: 26px; }

  .home p 
  { font-size: 19px; }

  .home img 
  { max-width: 600px; }
}

/* Desktop */
@media (min-width: 1024px) 
{
  .home h1
  { font-size:  40px ; }

  .home p
  { font-size:  20px ; }
}
</style>