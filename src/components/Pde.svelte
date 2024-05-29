<svelte:head>
	<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/katex@0.12.0/dist/katex.min.css" integrity="sha384-AfEj0r4/OFrOo5t7NnNe46zW/tFgW6x/bCJG8FqQCEo3+Aro6EYUG4+cU+KJWu/X" crossorigin="anonymous">
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@4.4.1/dist/css/bootstrap.min.css" integrity="sha384-Vkoo8x4CGsO3+Hhxv8T/Q5PaXtkKtu6ug5TOeNV6gBiFeWPGFN9MuhOf23Q9Ifjh" crossorigin="anonymous">
</svelte:head>

<script>
  import katexify from '../katexify';
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
    </div>
  </div>
</main>

<style>
  @import 'styles.css';
</style>