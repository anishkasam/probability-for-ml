<svelte:head>
	<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/katex@0.12.0/dist/katex.min.css" integrity="sha384-AfEj0r4/OFrOo5t7NnNe46zW/tFgW6x/bCJG8FqQCEo3+Aro6EYUG4+cU+KJWu/X" crossorigin="anonymous">
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@4.4.1/dist/css/bootstrap.min.css" integrity="sha384-Vkoo8x4CGsO3+Hhxv8T/Q5PaXtkKtu6ug5TOeNV6gBiFeWPGFN9MuhOf23Q9Ifjh" crossorigin="anonymous">
</svelte:head>

<script>
  import katexify from '../katexify';
</script>

<main>
  <div id="expvar" class="section">
    <h2 class="section-header">Expectation & Variance</h2>

    <div class="subsection">
      <h4 class="subsection-header">Expectation of Discrete Random Variables</h4>

      <p>Suppose {@html katexify("X", false)} is a discrete random variable with pmf 
      {@html katexify("p_x", false)}. Its expectation (also known as mean/average) is given by:</p>

      {@html katexify("\\mathbb{E}\\text{[X]}=\\sum_{a\\in\\R}a\\cdot p_x(a)=\\sum_{a\\in\\R}a\\cdot \\mathbb{P}(X=a)", true)}
    
      <p>Suppose {@html katexify("W\\sim \\text{Ber}(p)", false)}. Then, 
      {@html katexify("\\mathbb{E}\\text{[W]}=p", false)}.</p>

      <p>Suppose {@html katexify("X\\sim \\text{Bin}(n,p)", false)}. Then, 
      {@html katexify("\\mathbb{E}\\text{[X]}=np", false)}.</p>

      <p>Suppose {@html katexify("Y\\sim \\text{Geom}(p)", false)}. Then, 
      {@html katexify("\\mathbb{E}\\text{[Y]}=\\frac{1}{p}", false)}.</p>

      <p>Suppose {@html katexify("Z\\sim \\text{Poisson}(\\lambda)", false)}. Then, 
      {@html katexify("\\mathbb{E}\\text{[Z]}=\\lambda", false)}.</p>

      <p><b>Theorem:</b> expecation is linear; if {@html katexify("X", false)} and 
      {@html katexify("\\text{Y}", false)} are random variables defined on the same probability space
      and {@html katexify("c\\in\\R", false)}, then 
      {@html katexify("\\mathbb{E}\\text{[X}+\\text{Y]}=\\mathbb{E}\\text{[X]}+\\mathbb{E}\\text{[Y]}", false)}
      and {@html katexify("\\mathbb{E}\\text{[cX]}=c\\mathbb{E}\\text{[X]}", false)}.</p>

      <p><b>Theorem:</b> if {@html katexify("X", false)} is a discrete random variable and
      {@html katexify("g", false)} is a function, then  
      {@html katexify("\\mathbb{E}\\text{[g(X)]}=\\sum_{a\\in\\R}g(a)\\cdot\\mathbb{P}(X=a)", false)}.</p>
    </div>
    
    <div class="subsection">
      <h4 class="subsection-header">Expectation of Continuous Random Variables</h4>

      <p>Suppose {@html katexify("X", false)} is a continuous random variable with pdf 
      {@html katexify("f_x", false)}. Its expectation is given by:</p>

      {@html katexify("\\mathbb{E}\\text{[X]}=\\int^{\\infty}_{-\\infty}t\\cdot f_x(t)dt", true)}
    
      <p>Suppose {@html katexify("U\\sim \\text{Unif}[a,b]", false)}. Then, 
      {@html katexify("\\mathbb{E}\\text{[U]}=\\frac{a+b}{2}", false)}.</p>

      <p>Suppose {@html katexify("X\\sim \\mathcal{N}(\\mu,\\sigma)", false)}. Then, 
      {@html katexify("\\mathbb{E}\\text{[X]}=\\mu", false)}.</p>

      <p><b>Theorem:</b> if {@html katexify("X", false)} is a continuous random variable and
      {@html katexify("g", false)} is a function, then  
      {@html katexify("\\mathbb{E}\\text{[g(X)]}=\\int^{\\infty}_{-\\infty}g(t)f_x(t)dt", false)}.</p>
    </div>

    <div class="subsection">
      <h4 class="subsection-header">Variance</h4>

      <p>Let {@html katexify("X", false)} be a random variable. The variance of {@html katexify("X", false)} is:</p>

      {@html katexify("\\text{Var}\\text{(X)}=\\mathbb{E}[(X-\\mathbb{E}\\text{[X]})^2]=\\mathbb{E}[X^2]-(\\mathbb{E}\\text{[X]})^2", true)}
    
      <p>The standard deviation of {@html katexify("X", false)} is: {@html katexify("\\sqrt{\\text{Var}(X)}", false)}.</p>
    </div>
  </div>
</main>

<style>
  @import 'styles.css';
</style>