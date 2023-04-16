<script>
  // Dimensions
  const width = 800;
  const height = 100;
  const margin = { top: 5, right: 5, bottom: 20, left: 5 };
  const innerWidth = width - margin.left - margin.right;
  const innerHeight = height - margin.top - margin.bottom;

  // Scales
  import { scaleLog } from 'd3-scale';
  import { axisBottom } from 'd3-axis';
  import { select } from 'd3-selection';

  const xScale = scaleLog()
    .domain([1, 10])
    .range([0, innerWidth]);

  const values = [2, 4, 6, 7, 9];

  function createXAxis(handle) {
    const xAxis = axisBottom(xScale);
    select(handle).call(xAxis);

    select(handle)
      .append("text")
      .attr("x", innerWidth / 2)
      .attr("y", margin.bottom - 5)
      .attr("fill", "currentColor")
      .attr("text-anchor", "middle")
      .text("X Axis");
  }
</script>

<svg viewBox={`0 0 ${width} ${height}`}>
  <g transform={`translate(${margin.left},${margin.top})`} />
  <g transform={`translate(${margin.left},${innerHeight + margin.top})`} use:createXAxis />
  {#each values as value}
    <circle cx={xScale(value)} cy={innerHeight/2} r=10 />
  {/each}
</svg>
