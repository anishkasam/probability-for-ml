<svelte:head>
	<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/katex@0.12.0/dist/katex.min.css" integrity="sha384-AfEj0r4/OFrOo5t7NnNe46zW/tFgW6x/bCJG8FqQCEo3+Aro6EYUG4+cU+KJWu/X" crossorigin="anonymous">
	<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@4.4.1/dist/css/bootstrap.min.css" integrity="sha384-Vkoo8x4CGsO3+Hhxv8T/Q5PaXtkKtu6ug5TOeNV6gBiFeWPGFN9MuhOf23Q9Ifjh" crossorigin="anonymous">
</svelte:head>

<script>
	import { onMount } from 'svelte';
	import katexify from '../katexify';
	import * as d3 from 'd3';

	let h = 0.25; // Initial value for bandwidth
	let n = 1;    // Initial value for number of data points
	let data;
	let svg;
	const width = 500;
	const height = 300;
	const margin = { top: 20, right: 30, bottom: 30, left: 40 };

	function generateData(n) {
		return d3.range(n).map(d3.randomNormal(1));
	}

	function updateChart() {
		if (!svg) return;

		const x = d3.scaleLinear().domain([-1, 2.5]).range([margin.left, width - margin.right]);
		const y = d3.scaleLinear().domain([0, 1.5]).range([height - margin.bottom, margin.top]);

		const kde = kernelDensityEstimator(kernelGaussian(h), x.ticks(100));
		const density = kde(data);

		svg.selectAll("*").remove();

		svg.append("g")
			.attr("fill", "none")
			.attr("stroke", "steelblue")
			.attr("stroke-width", 2) // Thicker line
			.selectAll("path")
			.data([density])
			.join("path")
			.attr("d", d3.line()
				.curve(d3.curveBasis)
				.x(d => x(d[0]))
				.y(d => y(d[1]))
			);

		svg.append("g")
			.attr("transform", `translate(0,${height - margin.bottom})`)
			.call(d3.axisBottom(x).ticks(0)); // Remove the numbers from the x-axis

		svg.append("g")
			.attr("transform", `translate(${margin.left},0)`)
			.call(d3.axisLeft(y).ticks(0)); // Remove the numbers from the y-axis
	}

	function kernelDensityEstimator(kernel, X) {
		return function (V) {
			return X.map(function (x) {
				return [x, d3.mean(V, function (v) { return kernel(x - v); })];
			});
		};
	}

	function kernelGaussian(h) {
		return function (u) {
			return Math.abs(u /= h) <= 1 ? (1 / (Math.sqrt(2 * Math.PI))) * Math.exp(-0.5 * u * u) / h : 0;
		};
	}

	onMount(() => {
		data = generateData(n);
		svg = d3.select("#chart")
			.append("svg")
			.attr("viewBox", [0, 0, width, height]);

		updateChart();
	});
</script>

<main>
  <div class="section" id="kde">
    <h2 class="section-header">Gaussian Kernel Density Estimators (KDE)</h2>

    <div class="subsection">
      <h4 class="subsection-header">Intuition</h4>

      <p>Gaussian kernel density estimators are another intuitive density estimation technique. The main idea is to place a 
      kernel function, in this case a normalized Gaussian, at every data point. The sum of all of these Gaussians will result 
      in a valid density function that is more appealing than the one derived using a histogram estimator.</p>

      <p>The kernel function is a Gaussian with a mean of {@html katexify("0", false)} and a variance of {@html katexify("1", false)}; 
      its pdf is given by:</p>

      {@html katexify("K(x)=\\frac{1}{\\sqrt{2\\pi}}e^\\frac{-x^2}{2}", true)}

      <p>The overall density function is given by:</p>

      {@html katexify("f(x)=\\frac{1}{nh}\\sum^n_{i=1}K(\\frac{x-x_i}{h})", true)}

      <p>In this equation, {@html katexify("\\frac{1}{n}", false)} ensures that the sum of all {@html katexify("n", false)} Gaussians is normalized, maintaining an area of {@html katexify("1", false)}. Additionally, {@html katexify("h", false)} controls the width of each Gaussian.</p>
    </div>

    <div class="subsection">
      <h4 class="subsection-header">KDE Example</h4>

      <div id="chart"></div>

      <div>
        <label for="bandwidth">Bandwidth (h):</label>
        <input type="range" id="bandwidth" min="0.01" max="1" step="0.01" bind:value={h} on:input={updateChart}>
        <span>{h}</span>
      </div>
      <div>
        <label for="num-points">Number of Data Points (n):</label>
        <input type="range" id="num-points" min="1" max="100" step="1" bind:value={n} on:input={() => { data = generateData(n); updateChart(); }}>
        <span>{n}</span>
      </div>
    </div>

    <div class="subsection">
      <h4 class="subsection-header">Pros & Cons of KDE Estimators</h4>

      <p>Just like histogram estimators, KDE estimators are easy to understand and don't make assumptions about the data. Additionally,
      KDE estimators address some of the key issues with histogram estimators. Unlike histogram estimators, they produce a smooth
      estimate of the density function.</p>

      <p>However, KDE estimators have their own set of disadvantages. Firstly, they're computationally expensive; computing a Gaussian
      for each data point can be very costly especially if the data set is massive. Furthermore, they still need a substantial amount of data,
      albeit less than histogram estimators to provide accurate estimates.</p>
    </div>
  </div>
</main>

<style>
	@import 'styles.css';

	#chart {
		margin-top: 20px;
	}
</style>
