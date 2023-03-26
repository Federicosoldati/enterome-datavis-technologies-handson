<script>
  let current = "";
</script>
<style>
  .bluecolor {
background-color: lightsalmon;
  }
</style>

<!-- We will cover buttons later on! -->
<button class="btn btn-secondary" class:bluecolor={current=="messi"} on:click={() => (current = "messi")}>
  Messi
</button>

<button class="btn btn-secondary" class:bluecolor={current=="ronaldo"} on:click={() => (current = "ronaldo")}>
  Ronaldo
</button>

<button class="btn btn-secondary" class:bluecolor={current=="neymar"} on:click={() => (current = "neymar")}>
  Neymar
</button>