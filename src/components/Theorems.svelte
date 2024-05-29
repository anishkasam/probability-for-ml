<svelte:head>
	<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/katex@0.12.0/dist/katex.min.css" integrity="sha384-AfEj0r4/OFrOo5t7NnNe46zW/tFgW6x/bCJG8FqQCEo3+Aro6EYUG4+cU+KJWu/X" crossorigin="anonymous">
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@4.4.1/dist/css/bootstrap.min.css" integrity="sha384-Vkoo8x4CGsO3+Hhxv8T/Q5PaXtkKtu6ug5TOeNV6gBiFeWPGFN9MuhOf23Q9Ifjh" crossorigin="anonymous">
</svelte:head>

<script>
  import katexify from '../katexify';
</script>

<main>
  <div id="theorems" class="section">
    <h2 class="section-header">Important Theorems</h2>
    
    <div class="subsection">
      <h4 class="subsection-header">Central Limit Theorem</h4>

      <p>Suppose {@html katexify("X_1,X_2,...", false)} is an infinite sequence of independent and
      identically distributed random variables with mean {@html katexify("\\mu", false)} and variance
      {@html katexify("\\sigma^2", false)}. Let {@html katexify("S_n=X_1+X_2+...+X_n", false)}. Then:</p>

      {@html katexify("\\lim_{n\\to\\infty}\\frac{S_n-n\\mu}{\\sigma\\sqrt{n}}\\sim\\mathcal{N}(0,1)", true)}
    </div>
  
      <div class="subsection">
      <h4 class="subsection-header">Law of Large Numbers</h4>
      
      <p>Suppose {@html katexify("X_1,X_2,...", false)} is an infinite sequence of independent and
      identically distributed random variables with mean {@html katexify("\\mu", false)} and finite variance.
      Then:</p>

      {@html katexify("\\mathbb{P}(\\lim_{n\\to\\infty}\\overline{X}_n=\\mu)=1", true)}
    </div>
  </div>
</main>

<style>
  @import 'styles.css';
</style>