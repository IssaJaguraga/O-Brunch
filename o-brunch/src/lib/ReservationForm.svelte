 


<script>
  let name = "";
  let date = "";
  let guests = 1;

  const submitForm = () => {
    alert(`Merci ${name}, votre réservation pour ${guests} personne(s) le ${date} est confirmée !`);
    // ici tu pourrais connecter une API ou une DB réelle plus tard
    name = "";
    date = "";
    guests = 1;
  };
</script>

<section class="reservation">
  <h2>Réserver une table</h2>
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
  }
  button:hover {
    background-color: #a17845;
  }
</style>