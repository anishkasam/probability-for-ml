<svelte:head>
	<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/katex@0.12.0/dist/katex.min.css" integrity="sha384-AfEj0r4/OFrOo5t7NnNe46zW/tFgW6x/bCJG8FqQCEo3+Aro6EYUG4+cU+KJWu/X" crossorigin="anonymous">
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@4.4.1/dist/css/bootstrap.min.css" integrity="sha384-Vkoo8x4CGsO3+Hhxv8T/Q5PaXtkKtu6ug5TOeNV6gBiFeWPGFN9MuhOf23Q9Ifjh" crossorigin="anonymous">
</svelte:head>

<script>
  import katexify from '../katexify';

  import { onMount } from 'svelte';
  import { onDestroy } from 'svelte';
  import * as d3 from 'd3';
  import { range } from "d3-array";
  import { line } from "d3-shape";

  let numDataPoints = 1000;
  let allData = [];
  let data = [];
  let bins = [];
  let height = 500;
  let width;
  let windowWidth;

  function gaussian(x, mu, sigma) {
    return (1 / (sigma * Math.sqrt(2 * Math.PI))) * Math.exp(-((x - mu) ** 2) / (2 * sigma ** 2));
  }

  const generateInitialData = () => {
    const randomNormal = d3.randomNormal(0, 1);
    allData = Array.from({ length: 10000 }, randomNormal);
    updateData();
  };

  const updateData = () => {
    data = allData.slice(0, numDataPoints);
    createHistogram();
  };

  const createHistogram = () => {
    const numBins = Math.max(20, Math.floor(numDataPoints / 100));
    const x = d3.scaleLinear().domain([-3, 3]).range([0, width - width / (bins.length + 1)]);

    const histogram = d3.histogram()
      .domain(x.domain())
      .thresholds(x.ticks(numBins));

    bins = histogram(data);
  };

  onMount(() => {
    generateInitialData();

    windowWidth = window.innerWidth;
    width = Math.min(0.8 * windowWidth, 800);

    const updateWidth = () => {
      windowWidth = window.innerWidth;
      width = Math.min(0.8 * windowWidth, 800);
    };

    window.addEventListener('resize', updateWidth);
  });

</script>

<main>
  <div id="npde" class="section">
    <h2 class="section-header">Nonparametric Density Estimation</h2>
    
    <div class="subsection">
      <h4 class="subsection-header">Histogram Estimators</h4>

      <p>Histogram estimators are the simplest density estimation technique.
      Data is split up into non-overlapping bins and the number of data points
      in each bin is counted. These counts are then normalized (scaled down)
      so that the resulting histogram is a valid density function.</p>

      <p>When estimating density at a specific value, the height of the bin
      containing that value is used.</p>

      <svg width=width height="501">
        {#each bins as bin}
          <g transform={`translate(${d3.scaleLinear().domain([-3, 3]).range([0, width - width / (bins.length + 1)])(bin.x0)},${d3.scaleLinear().domain([0, d3.max(bins, d => d.length / (numDataPoints * bin.length))]).range([500, 0])(bin.length / (numDataPoints * bin.length))})`} class="bar">
            <rect width={width / (bins.length) + 1} height={width - d3.scaleLinear().domain([0, d3.max(bins, d => d.length / (numDataPoints * bin.length))]).range([500, 0])(bin.length / (numDataPoints * bin.length))} />
          </g>

          <line x1="0" y1="500" x2="800" y2="500" stroke="#000000" stroke-opacity="1" stroke-width="1"/>
        {/each}

      </svg>

      <label>
        Number of Data Points:
        <input type="range" bind:value={numDataPoints} min="1000" max="10000" step="1000" on:input={updateData} />
      </label>

      <p>The main advantages of using a histogram estimator is that they are
      very easy to implement and don't make any assumptions
      about the underlying distribution of the data.</p>

      <p>However, histogram estimators also have a few disadvantages. In order
      to construct a good estimate, you need a lot of data points; ideally every
      bin will have atleast one data point. In low dimensions, this is feasible,
      however, once you start working with high-dimensional data, the number of bins
      increases exponentially.</p>
    </div>
  </div>
</main>

<style>
  @import 'styles.css';

  .bar {
    fill: #2980b9;
  }
  svg {
    margin-bottom: 50px;
  }
</style>