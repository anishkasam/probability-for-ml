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
    <h2 class="section-header">Density Estimation in Practice</h2>

    <div class="subsection">
      <h4 class="subsection-header">Classification</h4>
      
      <p>In practice, density estimation is a powerful technique for classification. By fitting separate density estimates 
      for each class based on the data you have, you can use these estimates to predict the class of new data points. 
      When predicting, you compute the probability that a new point belongs to each class based on the fitted densities. 
      You then predict the class that is most likely to produce the given data point.</p>
    </div>

    <div class="subsection">
      <h4 class="subsection-header">Histogram, KDE, or MLE?</h4>
      
      <p>All three density estimation techniques have their own advantages and disadvantages.
      Well which one should be used? That depends on the data and the task at hand.</p>

      <p>In specific scenarios, each one can be the best option. For example, if you have
      a vast amount of data, histogram estimators could be the best. If you have data that
      is almost guaranteed to be from a known distribution, MLE might be the best. On the other
      hand if you have data that comes from an unknown distribution, KDE could be appropriate.</p>

      <p>In practice, it's important to tailor your approach to the characteristics of your data
      and the objectives of your analysis.</p>
    </div>

    <div class="subsection">
      <h4 class="subsection-header">Data Quality</h4>

      <p>Regardless of whether you choose a parametric or nonparametric method of density
      estimation, the data being used to fit the density is incredibly important. Specifically,
      it's important that the data is representative of the population. Otherwise, the 
      estimated density won't be representative of the population either.</p>

      <p>Data is typically collected through sampling, and there are three main methodologies:</p>

      <p><b>Simple Random Sampling:</b> each member of the population has an equal chance
      of being selected, oftentimes a random number generator is used.</p>

      <p><b>Stratified Random Sampling:</b> the population is divided into non-overlapping 
      groups called strata. Within each strata, members are sampled using simple random
      sampling.</p>

      <p><b>Clustered Random Sampling:</b> the population is divided into non-overlapping groups 
      called clusters. Clusters are then sampled at random, and all members of selected clusters 
      are part of the final sample.</p>
      
      <p>Stratified sampling often ensures a more representative sample since subgroups are 
      guaranteed to be sampled from. Clustered sampling on the other hand sacrifies 
      representation for cost effectiveness, since sampling entire clusters at once can be
      less expensive.</p>
    </div>

    <div>
      <h4 class="subsection-header">Sampling Visualized</h4>

      <p>The following visualization depicts how the population is partitioned when different
      sampling techniques are employed.</p>

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

  <div id="conclusion" class="section">
    <h2 class="section-header">Conclusion</h2>

    <div class="subsection">
      <p>All in all, density estimation is an incredibly powerful technique that can be adapted 
      for a wide variety of use cases. It's the foundation of many statistical and machine 
      learning methods. By selecting and applying the appropriate technique, be it histogram 
      estimators, KDEs, or MLEs you can uncover valuable insights, improve predictive models, 
      and make informed decisions based on your data.</p>
    </div>
  </div>

  <div id="sources" class="section">
    <h2 class="section-header">Sources</h2>

    <div class="subsection">
      <p>The explanations and visualizations for histogram estimators and maximum likelihood 
      estimation were adapted from Professor Justin Eldridge's <a href="https://dsc140a.com/">
      DSC 140A - Probabilistic Modeling & Machine Learning</a>.</p>

      <p>The explanations for kernel density estimators were adapted from Jaroslaw Drapala's 
      article, <a href="https://towardsdatascience.com/kernel-density-estimation-explained-step-by-step-7cc5b5bc4517">
      Kernel Density Estimator Explained</a>.</p>
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
