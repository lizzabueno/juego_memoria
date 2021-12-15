<script>
  function shuffle(array) {
    let currentIndex = array.length,
      randomIndex;

    // While there remain elements to shuffle...
    while (currentIndex != 0) {
      // Pick a remaining element...
      randomIndex = Math.floor(Math.random() * currentIndex);
      currentIndex--;

      // And swap it with the current element.
      [array[currentIndex], array[randomIndex]] = [
        array[randomIndex],
        array[currentIndex],
      ];
    }

    return array;
  }

  const opciones = [
    "🍏",
    "🍏",
    "🙀",
    "🙀",
    "🦤",
    "🦤",
    "🐧",
    "🐧",
    "🦜",
    "🦜",
    "🐍",
    "🐍",
    "🦔",
    "🦔",
    "🐰",
    "🐰",
    "🦣",
    "🦣",
    "🐒",
    "🐒",
    "🦝",
    "🦝",
    "🐣",
    "🐣",
    "🦉",
    "🦉",
    "🐠",
    "🐠",
    "🐛",
    "🐛",
    "🐌",
    "🐌",
    "🐙",
    "🐙",
    "🦖",
    "🦖",
  ];
  const aleatorio = shuffle(opciones);
  let primero = null;
  let segundo = null;
  let visibles = [];
  let intentos = 0;

  function revelar(indice) {
    if (primero == null) {
      primero = indice;
    } else if (segundo == null) {
      segundo = indice;
      verificar();
      intentos = intentos + 1;
      setTimeout(() => {
        primero = null;
        segundo = null;
      }, 500);
    }
  }

  function verificar() {
    const primerElemento = aleatorio[primero];
    const segundoElemento = aleatorio[segundo];
    if (primerElemento == segundoElemento) {
      visibles.push(primerElemento);
    }
  }
</script>

<main>
  {#each aleatorio as opcion, i}
    <button class="caja" on:click={() => revelar(i)} disabled={primero == i || segundo == i || visibles.includes(opcion)}>
      {#if primero == i || segundo == i || visibles.includes(opcion)}
        {opcion}
      {/if}
	</button>
  {/each}
  <p>
    intentos: {intentos}
  </p>
</main>

<style>
  .caja {
    border: 1px solid black;
    height: 40px;
    width: 40px;
    margin-top: 10px;
    margin-left: 5px;
    display: flex;
    align-items: center;
    justify-content: center;
  }
  main {
    display: flex;
    max-width: 550px;
    flex-wrap: wrap;
  }
</style>
