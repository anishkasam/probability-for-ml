<svelte:head>
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/katex@0.12.0/dist/katex.min.css" integrity="sha384-AfEj0r4/OFrOo5t7NnNe46zW/tFgW6x/bCJG8FqQCEo3+Aro6EYUG4+cU+KJWu/X" crossorigin="anonymous">
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@4.4.1/dist/css/bootstrap.min.css" integrity="sha384-Vkoo8x4CGsO3+Hhxv8T/Q5PaXtkKtu6ug5TOeNV6gBiFeWPGFN9MuhOf23Q9Ifjh" crossorigin="anonymous">
  <script src="https://d3js.org/d3.v6.min.js"></script>
</svelte:head>

<script>
  import { onMount } from "svelte";
  import * as d3 from 'd3';

  function gaussian(mean, variance) {
    return x => (1 / Math.sqrt(2 * Math.PI * variance)) * Math.exp(-((x - mean) ** 2) / (2 * variance));
  }

  onMount(() => {
    const width = 850;
    const height = 500;
    const margin = { top: 50, right: 50, bottom: 70, left: 75 };

    const x = d3.scaleLinear()
      .domain([-10, 10])
      .range([margin.left, width - margin.right]);

    const y = d3.scaleLinear()
      .domain([0, 0.5])
      .range([height - margin.bottom, margin.top]);

    const svg = d3.select("#ip")
      .append("svg")
      .attr("width", width)
      .attr("height", height);

    const gaussian1 = gaussian(-2, 1);
    const gaussian2 = gaussian(2, 1.5);

    const data1 = d3.range(-10, 10, 0.1).map(x => ({ x: x, y: gaussian1(x) }));
    const data2 = d3.range(-10, 10, 0.1).map(x => ({ x: x, y: gaussian2(x) }));

    const line = d3.line()
      .x(d => x(d.x))
      .y(d => y(d.y));

    svg.append("path")
      .datum(data1)
      .attr("fill", "#3498db")
      .attr("stroke", "#2980b9")
      .attr("opacity", 0.85)
      .attr("stroke-width", 2)
      .attr("d", line);

    svg.append("path")
      .datum(data2)
      .attr("fill", "#e74c3c")
      .attr("stroke", "#c0392b")
      .attr("opacity", 0.75)
      .attr("stroke-width", 2)
      .attr("d", line);

    svg.append("g")
      .attr("transform", `translate(0,${height - margin.bottom})`)
      .call(d3.axisBottom(x).ticks(8).tickSize(10))
      .append("text")
      .attr("fill", "#000")
      .attr("x", margin.left / 2 + width / 2)
      .attr("y", -height / 2 + 300)
      .attr("font-size", "18px")
      .attr("font-family", "Inter")
      .text("Feature");

    svg.append("g")
      .attr("transform", `translate(${margin.left},0)`)
      .call(d3.axisLeft(y).ticks(5).tickSize(10))
      .append("text")
      .attr("fill", "#000")
      .attr("transform", "rotate(-90)")
      .attr("y", margin.left / 2 - 75)
      .attr("x", -height / 2)
      .attr("font-size", "18px")
      .attr("font-family", "Inter")
      .text("Density")
      .attr("text-anchor", "middle");

    svg.append("text")
      .attr("x", 650)
      .attr("y", 150)
      .attr("fill", "black")
      .attr("font-size", "18")
      .attr("font-family", "Inter")
      .attr("text-anchor", "middle")
      .text("Density for Class 1");

    svg.append("defs")
      .append("marker")
      .attr("id", "arrowhead")
      .attr("markerWidth", 10)
      .attr("markerHeight", 7)
      .attr("refX", 0)
      .attr("refY", 3.5)
      .attr("orient", "auto")
      .append("polygon")
      .attr("points", "0 0, 3.5 3.5, 0 7");

    svg.append("path")
      .attr("d", "M650,160 C630,215 610,240 560,250")
      .attr("stroke", "black")
      .attr("stroke-width", 2)
      .attr("fill", "none")
      .attr("marker-end", "url(#arrowhead)");

    svg.append("text")
      .attr("x", 220)
      .attr("y", 150)
      .attr("fill", "black")
      .attr("font-size", "18")
      .attr("font-family", "Inter")
      .attr("text-anchor", "middle")
      .text("Density for Class 0");

    svg.append("defs")
      .append("marker")
      .attr("id", "arrowhead")
      .attr("markerWidth", 10)
      .attr("markerHeight", 7)
      .attr("refX", 0)
      .attr("refY", 3.5)
      .attr("orient", "auto")
      .append("polygon")
      .attr("points", "0 0, 3.5 3.5, 0 7");

    svg.append("path")
      .attr("d", "M220,160 C240,215 260,240 310,250")
      .attr("stroke", "black")
      .attr("stroke-width", 2)
      .attr("fill", "none")
      .attr("marker-end", "url(#arrowhead)");
  });
</script>

<main>
  <div id="sampling" class="section">
    <h2 class="section-header">Density Estimation in Practice</h2>

    <div class="subsection">
      <h4 class="subsection-header">Classification</h4>
      
      <p>One common technique for classification is to fit a separate density for each class. When predicting the class of a new data point, 
      you compute the probability that the data point belongs to each class based on these density estimates. This approach 
      forms the basis of techniques like Linear Discriminant Analysis (LDA) and Quadratic Discriminant Analysis (QDA). For example, a classification
      problem for a two class, one feature dataset could look like:</p>

      <div id="ip"></div>

      <p>Another common technique is to assume features are conditionally independent and then fit a separate density for each feature within
      each class. To predict the class of a new data point, you calculate the product of the probabilities of each feature given each class, 
      and select the class with the highest resulting value. This technique is known as the Naive Bayes classifier.</p>
    </div>
  </div>
</main>

<style>
  @import 'styles.css';

  #ip {
    margin-top: -30px;
    font-size: 18px;
    margin-left: -20px;
  }
</style>
