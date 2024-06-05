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

  let windowWidth;

  function generateData(n = 10) {
    const randomNormal = (mu, sigma) => {
      let u = 0, v = 0;
      while (u === 0) u = Math.random();
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
    console.log(data.reduce((a, b) => a + b, 0));
    maxLikelihood = calculateLikelihood(data, 0, 1);
    currentLikelihood = calculateLikelihood(data, mu, sigma);

    windowWidth = window.innerWidth;

    const updateWidth = () => {
      windowWidth = window.innerWidth;
    };

    window.addEventListener('resize', updateWidth);
  });

  $: currentLikelihood = calculateLikelihood(data, mu, sigma);
</script>

<main>
  <div id="para-density-est" class="section">
    <h2 class="section-header">Parametric Density Estimation</h2>

    <div class="subsection">
      <h4 class="subsection-header">Maximum Likelihood Estimation (MLE)</h4>
      <svg height="400" >
        <!-- X Axis -->
        <line x1="0" y1="350" x2="{windowWidth}" y2="350" stroke="#000000" stroke-opacity="1" stroke-width="2"/>

        {#each data as point}
          <circle cx="{(point + 3) * 100}" cy="350" r="5" fill="white" stroke="black" stroke-width="2"/>
          <line x1="{(point + 3) * 100}" y1="345" x2="{(point + 3) * 100}" y2="{350 - gaussian(point, mu, sigma) * 400}" stroke="green" stroke-dasharray="4" stroke-width="2" />
        {/each}

        <path d="{line().x(d => (d + 3) * 100).y(d => 350 - gaussian(d, mu, sigma) * 400)(range(-3, 10, 0.01))}" fill="none" stroke="green" stroke-width="3" />
      </svg>

      <div class="input-container">
        <label>{@html katexify("\\mu", false)} (controls the Gaussian's center)
        <input type="range" min="-3" max="3" step="0.0001" bind:value="{mu}" />
        </label>
        <label>{@html katexify("\\sigma", false)} (controls the Gaussian's width)
        <input type="range" min="0.5" max="2" step="0.0001" bind:value="{sigma}" />
        </label>
      </div>

      <div style="display: flex; align-items: center; margin-top: 10px;" class="mle-bar">
        <span>Current Likelihood</span>
        <div style="border-width: 2px; border-style: solid; background: white; width: 100%; height: 20px; position: relative; margin-right: 10px;">
          <div style="background: green; width: {Math.min(currentLikelihood / maxLikelihood, 1) * 100}%; height: 100%;"></div>
        </div>
        <span>Max Likelihood</span>
      </div>
    </div>
  </div>
</main>

<style>
  svg {
    width: 100%;
  }

  input[type="range"] {
    width: 100%;
    margin: 10px 0;
    accent-color: green;
  }

  input[type="range"]:focus {
    accent-color: green;
  }

  .mle-bar {
    text-align: center;
  }
</style>
