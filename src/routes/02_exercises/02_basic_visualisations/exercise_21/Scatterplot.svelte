<script>
    import { schemeDark2 } from 'd3-scale-chromatic';
    import { scaleLinear, scaleSqrt, extent, scaleOrdinal } from 'd3-scale';
    export let data;
    
    // Dimensions
    const [height, width] = [400, 600];
    const margin = { top: 50, right: 5, bottom: 55, left: 50 };
    const innerWidth = width - margin.left - margin.right;
    const innerHeight = height - margin.top - margin.bottom;
    
    // Scales
    
    const xScale = scaleLinear()
      .domain(extent(data, d => +d.income))
      .range([0, innerWidth])
      .nice();

    const yScale = scaleLinear()
      .domain(extent(data, d => +d.life_exp))
      .range([innerHeight, 0])
      .nice();

    const rScale = scaleSqrt()
      .domain(extent(data, d => +d.population))
      .range([2, 20]);

    const colorScale = scaleOrdinal()
      .domain([...new Set(data.map(v => v.continent))])
      .range(schemeDark2);

  </script>
  
  <svg viewBox="0 0 {width} {height}" style="max-width: {width}px">
    <g transform="translate({margin.left}, {margin.top})">
      <g each={data}>
        <circle cx={xScale(data.income)} cy={yScale(data.life_exp)} r={rScale(data.population)} fill={colorScale(data.continent)} />
      </g>    
    </g>
  </svg>