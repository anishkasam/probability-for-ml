<!--
  @component
  Generates an SVG force simulation using [d3-force](https://github.com/d3/d3-force). The values here are defaults which you will likely have to customize because every force simulation is different. This technique comes from @plmrry.
-->
<script>
  import { getContext } from 'svelte';
  import {
    forceSimulation,
    forceX,
    forceManyBody,
    forceCollide,
    forceCenter,
  } from 'd3-force';

  const { data, width, height, xScale, xGet, rGet, zGet } = getContext('LayerCake');

  export let manyBodyStrength = 100;
  export let xStrength = 0;
  export let nodeColor = undefined;
  export let nodeStroke = 'black';
  export let nodeStrokeWidth = 2;
  export let groupBy = "1";

  const initialNodes = $data.map((d) => ({ ...d }));

  const simulation = forceSimulation(initialNodes)

  let nodes = [];

  simulation.on("tick", () => {
    nodes = simulation.nodes()
  })

  $: {
    simulation
      .force('x', forceX().x(d => {
        return groupBy === 1 ? $width / 2 : $xGet(d) + $xScale.bandwidth() / 2;
      }).strength(xStrength))
      .force('center', forceCenter($width / 2, $height / 2))
      .force('charge', forceManyBody().strength(manyBodyStrength))
      .force('collision', forceCollide().radius(d => {
        return $rGet(d) + nodeStrokeWidth / 2;
      }))
      .alpha(0.5)
      .restart()
  }

  $: xKey = groupBy === "3" ? 'cluster' : 'category';
</script>

  {#each nodes as point}
    <circle
      class='node'
      r={$rGet(point)}
      fill={nodeColor || $zGet(point)}
      stroke={nodeStroke}
      stroke-width={nodeStrokeWidth}
      cx='{point.x}'
      cy='{point.y}'
    >
    </circle>
  {/each}

<style>
  circle {
    transition: 0.125s;
  }
</style>