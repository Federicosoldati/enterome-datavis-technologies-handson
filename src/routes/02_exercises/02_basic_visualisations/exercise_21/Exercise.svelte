<script>
    import { onMount } from 'svelte';
    import Scatterplot from './Scatterplot.svelte';

    let countries = null;
    let dataLoaded = false;
    
    onMount(async () => {
      const response = await fetch('/data/gapminder.json');
      const data = await response.json();
      countries = data.filter(d => d.year === 1800).map(d => d.country);
      dataLoaded = true;
    });
</script>

{#if dataLoaded}
  <Scatterplot data={countries} />
{:else}
  <p>Loading data...</p>
{/if}