<svelte:head>
	<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/katex@0.12.0/dist/katex.min.css" integrity="sha384-AfEj0r4/OFrOo5t7NnNe46zW/tFgW6x/bCJG8FqQCEo3+Aro6EYUG4+cU+KJWu/X" crossorigin="anonymous">
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@4.4.1/dist/css/bootstrap.min.css" integrity="sha384-Vkoo8x4CGsO3+Hhxv8T/Q5PaXtkKtu6ug5TOeNV6gBiFeWPGFN9MuhOf23Q9Ifjh" crossorigin="anonymous">
</svelte:head>

<script>
  import katexify from '../katexify';
</script>

<main>
  <div id="crvs" class="section">
    <h2 class="section-header">Continuous Distributions</h2>

    <div class="subsection">
      <h4 class="subsection-header">Uniform Distributions</h4>

      <p>The uniform distribution is a probability distribution in which all outcomes
      are equally likely within a specified range, {@html katexify("[a,b]", false)}.</p>

      <p>Let {@html katexify("X", false)} be a uniform random variable. Then, we write 
      {@html katexify("X\\sim \\text{Unif}[a,b]", false)}. Its pdf is given by:</p>

      {@html katexify("f_x(t)=\\begin{cases} \\frac{1}{b-a},\\ t\\in[a,b] \\\\ 0,\\ t\\notin[a,b] \\end{cases}", true)}
    </div>
    
    <div class="subsection">
      <h4 class="subsection-header">Normal (Gaussian) Distributions</h4>

      <p>The normal distribution is a bell-shaped probability distribution defined by its mean, 
      {@html katexify("\\mu", false)} (the center) and its standard deviation, 
      {@html katexify("\\sigma", false)} (the spread).</p>

      <p>Let {@html katexify("X", false)} be a normal random variable. Then, we write 
      {@html katexify("X\\sim \\mathcal{N}(\\mu,\\sigma^2)", false)}. Its pdf is given by:</p>

      {@html katexify("f_x(t)=\\frac{1}{\\sqrt{2\\pi\\sigma^2}}e^{-\\frac{1}{2}(\\frac{t-\\mu}{\\sigma})^2}", true)}
    </div>
  </div>
</main>

<style>
  @import 'styles.css';
</style>