<svelte:head>
	<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/katex@0.12.0/dist/katex.min.css" integrity="sha384-AfEj0r4/OFrOo5t7NnNe46zW/tFgW6x/bCJG8FqQCEo3+Aro6EYUG4+cU+KJWu/X" crossorigin="anonymous">
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@4.4.1/dist/css/bootstrap.min.css" integrity="sha384-Vkoo8x4CGsO3+Hhxv8T/Q5PaXtkKtu6ug5TOeNV6gBiFeWPGFN9MuhOf23Q9Ifjh" crossorigin="anonymous">
</svelte:head>

<script>
  import katexify from '../katexify';
</script>

<main>
  <div id="npde" class="section">
    <h2 class="section-header">What is Density Estimation?</h2>
    
    <div class="subsection">
      <h4 class="subsection-header">Definiton</h4>
        
      <p>Density estimation is a technique used to estimate the probability density
      function that data came from. There are two main types of density 
      estimation:</p>

      <p><b>Nonparametric Density Estimation:</b> a technique where no assumptions
      are made about the underlying distribution of the data. Rather, the estimated
      density is fit to the data itself.</p>

      <p><b>Parametric Density Estimation:</b> a technique where the underlying
      distribution (ex: normal, exponential, etc.) that the data comes from is assumed. 
      The parameter(s) that maximize the likelihood of observing the given data are used to 
      estimate the density. </p>
    </div>

    <div class="subsection">
      <h4 class="subsection-header">Importance & Applications</h4>

      <p>Understanding the underlying distribution of data results in highly 
      useful insights. It's employed by many different machine learning methods
      including Naive Bayes classifiers and Markov models.</p>

      <p>These models have applications to countless different industries. They're
      used in finance for risk assessment and fraud detection; in healthcare for disease
      diagnosis and treatment personalization; and in agriculture for yield maximization 
      and pest control.</p>
    </div>
  </div>
</main>

<style>
  @import 'styles.css';
</style>