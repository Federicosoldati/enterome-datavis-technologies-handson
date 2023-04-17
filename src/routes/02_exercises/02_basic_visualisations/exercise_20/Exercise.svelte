<script>
    // Dimensions
    const width = 600;
    const height = 300;
    const margin = { top: 10, right: 10, bottom: 30, left: 60 };
    const innerWidth = width - margin.left - margin.right;
    const innerHeight = height - margin.top - margin.bottom;
  
    // Array
    const data = [
      { service: "Netflix", viewers: 2.9, x: "10" },
      { service: "Amazon Prime", viewers: 1.3 , x: "70" },
      { service: "Disney+", viewers: 2.1 , x: "130" },
      { service: "Hulu", viewers: 0.9 , x: "190" },
      { service: "Apple TV", viewers: 1.1 , x: "250" },
      { service: "Rakuten", viewers: 0.4 , x: "310" }
    ];

    // Scales
    import { scaleLinear } from 'd3-scale';
    import { scaleOrdinal } from 'd3-scale';
    import { schemeDark2 } from 'd3-scale-chromatic';
    import { axisLeft } from 'd3-axis';
    import { select } from 'd3-selection';
    import { axisBottom } from 'd3-axis';
    import { scalePoint } from 'd3-scale';
    
    const yScale = scaleLinear()
      .domain([0, 4])
      .range([innerHeight, 0]);

    const colorScale = scaleOrdinal()
      .domain([...new Set(data.map(v => v.service))])
      .range(schemeDark2);

    function createYAxis(handle) {
      const yAxis = axisLeft(yScale);
      select(handle).call(yAxis); 

      select(handle)
        .selectAll("text")
        .attr("font-size", 16);

      select(handle)
        .append("text")
        .attr("x", innerWidth-480)
        .attr("y", margin.bottom)
        .attr("fill", "currentColor")
        .attr("text-anchor", "middle")
        .text("Y Axis")
        .attr("font-size",25);
      }

  
    const xScale = scalePoint()
      .domain(data.map(d => d.service))
      .range([0, innerWidth])
      .padding(0.5);

    function createXAxis(handle) {
      const xAxis = axisBottom(xScale);
      select(handle).call(xAxis); 

      select(handle)
        .selectAll("text")
        .attr("font-size", 16);

      select(handle)
        .selectAll("text")
        .attr("x", xScale(value["service"]))
        .attr("y", margin.bottom - 20)
        .attr("fill", "currentColor")
        .attr("text-anchor", "middle")
        .text((d) => d)
        .attr("font-size", 20);
}

  </script>
  
  <!-- setting a viewBox and max-width allows the SVG to shrink but not grow! -->
  <svg viewbox="0 0 {width} {height}" style="max-width: {width}px">
    <g transform={`translate(${margin.left},${margin.top})`} use:createYAxis />
    <g transform={`translate(${margin.left},${innerHeight + margin.top})`} use:createXAxis />
    <g transform={`translate(${margin.left},${margin.top})`}>
      {#each data as value}
        <rect 
          x={xScale(value["service"])}
          y = {yScale(value["viewers"])}
          width={"20"}
          height={height - margin.bottom - margin.top - yScale(value["viewers"])}
          fill={colorScale(value["service"])}
        />
      {/each}
    </g>
  </svg>
  