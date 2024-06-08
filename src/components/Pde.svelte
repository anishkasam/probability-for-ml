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

  function gaussian(x, mu, sigma) {
    return (1 / (sigma * Math.sqrt(2 * Math.PI))) * Math.exp(-((x - mu) ** 2) / (2 * sigma ** 2));
  }

  function calculateLikelihood(data, mu, sigma) {
    return data.reduce((acc, point) => acc * gaussian(point, mu, sigma), 1);
  }

  function calculateAverage(data) {
    return data.reduce((sum, value) => sum + value, 0) / data.length;
  }

  function calculateStdDev(data, mean) {
    return Math.sqrt(data.reduce((sum, value) => sum + Math.pow(value - mean, 2), 0) / data.length);
  }

  onMount(() => {
    data = [-1.5, -1, -0.6, -0.3, -0.1, 0.1, 0.3, 0.6, 1, 1.5];
    console.log(data);
    console.log(data.reduce((a, b) => a + b, 0));
    maxLikelihood = calculateLikelihood(data, calculateAverage(data), calculateStdDev(data, calculateAverage(data)));
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
    <h2 class="section-header">Maximum Likelihood Estimators (MLE)</h2>

    <div class="subsection">
      <h4 class="subsection-header">Intuition</h4>
      
      <p>Unlike nonparametric density estimators, maximum likelihood estimators assume the 
      data follows a specific probability distribution. These distributions have parameters
      which define the characteristics of the distribution. For example, the parameters in a
      normal distribution are the mean (center) and standard deviation (spread).</p>

      <p>The optimal parameters are found by maximizing the likelihood function, which
      measures how probable the observed data is given values of parameters. It is defined as the
      product of the probability density functions for the observed data:</p>

      {@html katexify("L(\\theta ;x)=\\prod_{i=1}^n p_x(x_i|\\theta)", true)}
    </div>

    <div class="subsection">
      <h4 class="subsection-header">MLE Simulation</h4>

      <p>Try experimenting with different values of {@html katexify("\\mu", false)} (mean) and 
      {@html katexify("\\sigma", false)} (standard deviation) to find the parameter values 
      that maximize the likelihood of observing the data points below.</p>

      <svg height="375" style="position: relative;">
        <!-- X Axis -->
        <line x1="0" y1="350" x2="{windowWidth}" y2="350" stroke="#000000" stroke-opacity="1" stroke-width="2"/>
      
        <!-- Placeholder for data points and curve -->
        {#each data as point}
          <circle cx="{(point + 3) * 100}" cy="350" r="5" fill="white" stroke="black" stroke-width="2"/>
          <line x1="{(point + 3) * 100}" y1="345" x2="{(point + 3) * 100}" y2="{350 - gaussian(point, mu, sigma) * 400}" stroke="green" stroke-dasharray="4" stroke-width="2" />
        {/each}
      
        <path d="{line().x(d => (d + 3) * 100).y(d => 350 - gaussian(d, mu, sigma) * 400)(range(-3, 10, 0.01))}" fill="none" stroke="green" stroke-width="3" />

        <!-- Text beneath sliders -->
        <line x1="565" y1="45" x2="590" y2="45" stroke="green" stroke-width="3" stroke-dasharray="5,5" />
        <text x="675" y="50" font-size="18" text-anchor="middle">
          <tspan dx="5"> Likelihood at Point</tspan>
        </text>
      </svg>
      
      <div class="input-container">
        <label>
          <div>{@html katexify("\\mu", false)} (controls the Gaussian's center)</div>
          <input type="range" min="-1.4" max="3" step="0.00001" bind:value="{mu}" />
        </label>
      </div>

      <div class="input-container">
        <label>
          <div>{@html katexify("\\sigma", false)} (controls the Gaussian's width)</div>
          <input type="range" min="0.5" max="2" step="0.00001" bind:value="{sigma}" />
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

    <div class="subsection">
      <h4 class="subsection-header">Pros & Cons of MLE Estimators</h4>
      
      <p>One advantage of using MLE compared to nonparametric methods is the limited amount
      of data that it requires; since the distribution is already assumed, it just has to be fit.
      Another advantage comes from the fact that the assumed 
      distributions are already established. For example, if a normal distribution is assumed,
      then all of the useful properties of a normal distribution can be applied.</p>

      <p>The biggest disadvantage of using a maximum likelihood estimator has to do
      with the fact that it makes an assumption about the underlying distribution. If the
      data doesn't actually come from the assumed distribution, the estimated density can be
      wildly inaccurate, leading to misguided predictions.</p>
    </div>
  </div>
</main>

<style>
  svg {
    width: 100%;
  }

  input[type="range"] {
    width: 300px;
    accent-color: green;
  }

  input[type="range"]:focus {
    accent-color: green;
  }

  .mle-bar {
    text-align: center;
  }
</style>
