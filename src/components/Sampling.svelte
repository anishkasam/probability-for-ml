<svelte:head>
	<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/katex@0.12.0/dist/katex.min.css" integrity="sha384-AfEj0r4/OFrOo5t7NnNe46zW/tFgW6x/bCJG8FqQCEo3+Aro6EYUG4+cU+KJWu/X" crossorigin="anonymous">
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@4.4.1/dist/css/bootstrap.min.css" integrity="sha384-Vkoo8x4CGsO3+Hhxv8T/Q5PaXtkKtu6ug5TOeNV6gBiFeWPGFN9MuhOf23Q9Ifjh" crossorigin="anonymous">
</svelte:head>

<script>
  import katexify from '../katexify';
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
  </div>
</main>

<style>
  @import 'styles.css';
</style>