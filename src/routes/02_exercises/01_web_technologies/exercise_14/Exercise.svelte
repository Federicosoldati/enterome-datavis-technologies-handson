<script>
  let current = "";
  let lastClickedButton = null;
  
  const assignClass = (button) => {
    if (lastClickedButton !== null) {
      lastClickedButton.classList.remove("bg-color");
    }
    button.classList.add("bg-color");
    lastClickedButton = button;
  }
</script>

<!-- We will cover buttons later on! -->
<button class="btn btn-secondary" on:click={() => {current = "messi"; assignClass($event.target);}}>
  Messi
</button>

<button class="btn btn-secondary" on:click={() => {current = "ronaldo"; assignClass($event.target);}}>
  Ronaldo
</button>

<button class="btn btn-secondary" on:click={() => {current = "neymar"; assignClass($event.target);}}>
  Neymar
</button>

<style>
  .bg-color {
    background-color: #00ff00;
  }
</style>