<svelte:head>
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/katex@0.12.0/dist/katex.min.css" integrity="sha384-AfEj0r4/OFrOo5t7NnNe46zW/tFgW6x/bCJG8FqQCEo3+Aro6EYUG4+cU+KJWu/X" crossorigin="anonymous">
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@4.4.1/dist/css/bootstrap.min.css" integrity="sha384-Vkoo8x4CGsO3+Hhxv8T/Q5PaXtkKtu6ug5TOeNV6gBiFeWPGFN9MuhOf23Q9Ifjh" crossorigin="anonymous">
</svelte:head>

<script>
  import katexify from '../katexify';
  import { onMount } from 'svelte';
  import { LayerCake, Svg } from 'layercake';
  import { scaleOrdinal, scaleBand } from 'd3-scale';

  import ForceLayout from './CirclePackForce.svelte';

  const categories = ['cat1', 'cat2', 'cat3'];
  const clusters = ['clust1', 'clust2', 'clust3', 'clust4'];
  const data = [];

  let windowWidth;

  onMount(() =>{
    windowWidth = window.innerWidth;

    const updateWidth = () => {
      windowWidth = window.innerWidth;
    };

    window.addEventListener('resize', updateWidth);
  });

  for (let k = 0; k < 5; k++) {
    for (let i = 0; i < categories.length; i++) {
        for (let j = 0; j < clusters.length; j++) {
            const dataObject = {
                category: categories[i],
                cluster: clusters[j],
                value: 1
            };
            data.push(dataObject);
        }
    }
  }

  let groupBy = "1";

  const rKey = 'value';
  const zKey = 'category';

  const seriesColors = ['#e74c3c', '#2980b9', '#27ae60'];

  let manyBodyStrength = 15;
  let xStrength = 0.45;

  $: xKey = groupBy === "3" ? 'cluster' : 'category';
</script>

<main>
  <div id="sampling" class="section">
    <h2 class="section-header">Sampling</h2>

    <div class="subsection">
      <h4 class="subsection-header">Simple</h4>
      <p>In simple random sampling, each member of the population has an equal chance
      of being selected. Random number generators are often used to select members of
      the population.</p>
    </div>

    <div class="subsection">
      <h4 class="subsection-header">Stratified</h4>
      <p>In stratified random sampling, the population is divided into non-overlapping 
      groups called strata. Within each strata, members are sampled using simple random
      sampling.</p>
      <p>Stratified random sampling ensures that members from each strata are represented
      in the overall sample. </p>
    </div>

    <div class="subsection">
      <h4 class="subsection-header">Clustered</h4>
      <p>In clustered sampling, the population is divided into non-overlapping groups
      called clusters. Clusters are then sampled at random, and all members of selected
      clusters are part of the final sample.</p>
      <p>Clustered sampling can be easier to implement than other forms of sampling when 
      the population is large and spread out.</p>
    </div>

    <div>
      <h4 class="subsection-header">Simple vs. Stratified vs. Clustered</h4>

      <div class="input-container">
        <label><input type="radio" bind:group={groupBy} value="1"/>Simple</label>
        <label><input type="radio" bind:group={groupBy} value="2"/>Stratified</label>
        <label><input type="radio" bind:group={groupBy} value="3"/>Clustered</label>
      </div>

      <div class="chart-container">
        <LayerCake
          {data}
          x={xKey}
          r={rKey}
          z={zKey}
          xScale={scaleBand()}
          rRange={[5, Math.min(100, 10 + windowWidth / 200)]}
          zScale={scaleOrdinal()}
          zRange={seriesColors}
        >
          <Svg>
            <ForceLayout
              {manyBodyStrength}
              {xStrength}
              groupBy={JSON.parse(groupBy)}
            />
          </Svg>
        </LayerCake>
      </div>
    </div>
  </div>
</main>

<style>
  @import 'styles.css';

  .chart-container {
    width: 100%;
    height: 400px;
  }

  label {
    cursor: pointer;
  }

  input {
    margin-right: 7px;
  }

  .input-container {
    text-align: center;
    margin-top: 3vh;
  }

  label {
    margin-left: min(25px, 5vw);
    margin-right: min(25px, 5vw);
  }
</style>
