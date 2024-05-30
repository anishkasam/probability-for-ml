<script>
  import { onMount } from "svelte";
  import katexify from "../katexify";
  import { scaleLinear } from "d3-scale";
  import { range } from "d3-array";
  import { line } from "d3-shape";

  let mu = 0;
  let sigma = 0.5;
  let data = [];
  let maxLikelihood = 0;
  let currentLikelihood = 0;

  function generateData(n = 10) {
    const randomNormal = (mu, sigma) => {
      let u = 0, v = 0;
      while (u === 0) u = Math.random(); // Converting [0,1) to (0,1)
      while (v === 0) v = Math.random();
      return Math.sqrt(-2.0 * Math.log(u)) * Math.cos(2.0 * Math.PI * v) * sigma + mu;
    };
    return range(n).map(() => randomNormal(0, 1));
  }

  function gaussian(x, mu, sigma) {
    return (1 / (sigma * Math.sqrt(2 * Math.PI))) * Math.exp(-((x - mu) ** 2) / (2 * sigma ** 2));
  }

  function calculateLikelihood(data, mu, sigma) {
    return data.reduce((acc, point) => acc * gaussian(point, mu, sigma), 1);
  }

  onMount(() => {
    data = generateData();
    maxLikelihood = calculateLikelihood(data, 0, 1);
    currentLikelihood = calculateLikelihood(data, mu, sigma);
  });

  $: currentLikelihood = calculateLikelihood(data, mu, sigma);
</script>

<main>
  <div id="para-density-est" class="section">
    <h2 class="section-header">Parametric Density Estimation</h2>

    <div class="subsection">
      <h4 class="subsection-header">Method of Moments (MOM)</h4>
    </div>

    <div class="subsection">
      <h4 class="subsection-header">Maximum Likelihood Estimation (MLE)</h4>

      <p>Ideas: allow users to modify parameters of a normal distribution and calculate the
      likelihood of observing a set of data based on that</p>

      <svg width="800" height="400" viewBox="0 0 800 400">
        <!-- X Axis -->
        <line x1="50" y1="350" x2="750" y2="350" stroke="black" />
        <!-- Y Axis -->
        <line x1="50" y1="50" x2="50" y2="350" stroke="black" />

        {#each data as point}
          <circle cx="{50 + (point + 3) * 100}" cy="350" r="5" fill="white" stroke="black" />
          <line x1="{50 + (point + 3) * 100}" y1="350" x2="{50 + (point + 3) * 100}" y2="{350 - gaussian(point, mu, sigma) * 400}" stroke="green" stroke-dasharray="4" stroke-width="2" />
        {/each}

        <path d="{line().x(d => 50 + (d + 3) * 100).y(d => 350 - gaussian(d, mu, sigma) * 400)(range(-3, 3, 0.01))}" fill="none" stroke="green" stroke-width="2" />
      </svg>

      <div>
        <label>μ (controls the Gaussian's location)</label>
        <input type="range" min="-3" max="3" step="0.01" bind:value="{mu}" />
      </div>
      <div>
        <label>σ (controls the Gaussian's width)</label>
        <input type="range" min="0.48" max="3" step="0.01" bind:value="{sigma}" />
      </div>

      <div style="display: flex; align-items: center; margin-top: 10px;">
        <span>Current Likelihood</span>
        <div style="background: grey; width: 100%; height: 20px; position: relative; margin: 0 10px;">
          <div style="background: green; width: {Math.min(currentLikelihood / maxLikelihood, 1) * 100}%; height: 100%;"></div>
        </div>
        <span>Max Likelihood</span>
      </div>
    </div>
  </div>
</main>

<style>
  .section-header {
    font-size: 24px;
    margin-bottom: 20px;
  }
  .subsection-header {
    font-size: 20px;
    margin-bottom: 10px;
  }
  .section {
    margin: 20px;
  }
  svg {
    border: 1px solid black;
    margin-bottom: 20px;
  }
  input[type="range"] {
    width: 100%;
    margin: 10px 0;
  }
</style>
