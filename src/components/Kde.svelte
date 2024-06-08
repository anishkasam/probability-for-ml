<svelte:head>
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/katex@0.12.0/dist/katex.min.css" integrity="sha384-AfEj0r4/OFrOo5t7NnNe46zW/tFgW6x/bCJG8FqQCEo3+Aro6EYUG4+cU+KJWu/X" crossorigin="anonymous">
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@4.4.1/dist/css/bootstrap.min.css" integrity="sha384-Vkoo8x4CGsO3+Hhxv8T/Q5PaXtkKtu6ug5TOeNV6gBiFeWPGFN9MuhOf23Q9Ifjh" crossorigin="anonymous">
</svelte:head>

<script>
  import { onMount } from 'svelte';
  import katexify from '../katexify';
  import * as d3 from 'd3';

  function kde(kernel, thresholds, data) {
    return thresholds.map(t => [t, d3.mean(data, d => kernel(t - d))]);
  }

  function epanechnikov(bandwidth) {
    return x => Math.abs(x /= bandwidth) <= 1 ? 0.75 * (1 - x * x) / bandwidth : 0;
  }

  onMount(() => {
    let data = [-2.9, -1.8, -1.7, -1.6, -1.4, -1.3, -1.3, -0.7, 0, 0.4, 0.5, 0.6, 0.7, 0.8, 1.6, 1.7, 2.4, 2.5, 2.6, 2.7, 2.8, 3.4, 3.5]; 
    const width = 850;
    const height = 500;
    const margin = { top: 50, right: 50, bottom: 70, left: 75};

    const x = d3.scaleLinear()
      .domain([-4, 4])
      .range([margin.left, width - margin.right]);

    const y = d3.scaleLinear()
      .domain([0, 0.6])
      .range([height - margin.bottom, margin.top]);

    const svg = d3.select("#kde")
      .append("svg")
      .attr("width", width)
      .attr("height", height);

    const kdeData = kde(epanechnikov(0.5), x.ticks(100), data);

    const area = d3.area()
      .curve(d3.curveBasis)
      .x(d => x(d[0]))
      .y0(y(0))
      .y1(d => y(d[1]));

    svg.append("path")
      .attr("fill", "#e74c3c")
      .attr("stroke", "#c0392b")
      .attr("stroke-width", 2)
      .attr("opacity", 0.8)
      .attr("d", area(kdeData));

    svg.append("g")
      .attr("transform", `translate(0,${height - margin.bottom})`)
      .call(d3.axisBottom(x).ticks(8).tickSize(10))
      .append("text")
      .attr("fill", "#000")
      .attr("x", margin.left / 2 + width / 2)
      .attr("y", -height / 2 + 300)
      .attr("font-size", "18px")
      .attr("font-family", "Inter")
      .text("Measurement");

    svg.append("g")
      .attr("transform", `translate(${margin.left},0)`)
      .call(d3.axisLeft(y).ticks(5).tickSize(10)) // Increased axis number size
      .append("text")
      .attr("fill", "#000")
      .attr("transform", "rotate(-90)")
      .attr("y", margin.left / 2 - 75)
      .attr("x", -height / 2)
      .attr("font-size", "18px")
      .attr("font-family", "Inter")
      .text("Density")
      .attr("text-anchor", "middle");

    svg.append("g")
      .selectAll("circle")
      .data(data)
      .enter().append("circle")
      .attr("cx", d => x(d))
      .attr("cy", height - margin.bottom)
      .attr("r", 3)
      .attr("fill", "black")
      .attr("opacity", 0.6);
  });
</script>

<main>
  <div class="section">
    <h2 class="section-header">Gaussian Kernel Density Estimators (KDE)</h2>

    <div class="subsection">
      <h4 class="subsection-header">Intuition</h4>

    <p>However, sometimes a dataset does not follow that of a common density function. For example, in the graph below, it is clear that a simple Gaussian will not be sufficient to capture the nuances of this dataset. A more complex density estimator function will be needed to model this data.
    </p>
    <div id="kde"></div>
    <p>

      In datasets such as these, a Gaussian kernel density estimator can be used to represent a density function that will capture the data more accurately. The main idea is to place a kernel function,
      in this case a normalized Gaussian, at every data point. The sum of all
      of these Gaussians will result in a valid density function that is
      more appealing than the one derived using a histogram estimator.
    </p>

    <p>The kernel function is a Gaussian with a mean of {@html katexify("0", false)}
      and a variance of {@html katexify("1", false)}; its pdf is given by:
    </p>

    

    {@html katexify("K(x)=\\frac{1}{\\sqrt{2\\pi}}e^\\frac{-x^2}{2}", true)}

    <p>The overall density function is given by:</p>

    {@html katexify("f(x)=\\frac{1}{nh}\\sum^n_{i=1}K(\\frac{x-x_i}{h})", true)}

    <p>In this equation, {@html katexify("\\frac{1}{n}", false)} ensures that
      the sum of all {@html katexify("n", false)} Gaussians is normalized,
      maintaining an area of {@html katexify("1", false)}. Additionally,
      {@html katexify("h", false)} controls the width of each Gaussian.
    </p>
  </div>

  <div class="subsection">
    <h4 class="subsection-header">Pros & Cons of KDE Estimators</h4>

    <p>Just like histogram estimators, KDE estimators are easy to understand and don't make assumptions about the data. Additionally,
    KDE estimators address some of the key issues with histogram estimators. Unlike histogram estimators, they produce a smooth
    estimate of the density function.</p>

    <p>However, KDE estimators have their own set of disadvantages. Firstly, they're computationally expensive; computing a Gaussian
    for each data point can be very costly especially if the data set is massive. Furthermore, they still need a substantial amount of data,
    albeit less than histogram estimators, to provide accurate estimates.</p>
  </div>
  
</main>

<style>
  @import 'styles.css';
  
  .subsection {
    margin-bottom: 20px;
  }

  .subsection-header {
    margin-top: 20px;
  }

  #kde {
    margin-top: -30px;
    font-size: 18px;
    margin-left: -20px;
  }
</style>
