<svelte:head>
	<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/katex@0.12.0/dist/katex.min.css" integrity="sha384-AfEj0r4/OFrOo5t7NnNe46zW/tFgW6x/bCJG8FqQCEo3+Aro6EYUG4+cU+KJWu/X" crossorigin="anonymous">
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@4.4.1/dist/css/bootstrap.min.css" integrity="sha384-Vkoo8x4CGsO3+Hhxv8T/Q5PaXtkKtu6ug5TOeNV6gBiFeWPGFN9MuhOf23Q9Ifjh" crossorigin="anonymous">
</svelte:head>

<script>
  import katexify from '../katexify';
</script>

<main>
  <div id="drvs" class="section">
    <h2 class="section-header">Discrete Random Variables</h2>

    <div class="subsection">
      <h4 class="subsection-header">Bernoulli Random Variables</h4>

      <p>A Bernoulli random variable models a single experiment with two possible outcomes: success
      and failure. It has a success probability of {@html katexify("p", false)}.</p>

      <p>Let {@html katexify("X", false)} be a Bernoulli random variable. Then, we write 
      {@html katexify("X\\sim \\text{Ber}(p)", false)}. Its pmf is given by:</p>

      {@html katexify("\\mathbb{P}(X=1)=p", true)}
      {@html katexify("\\mathbb{P}(X=0)=1-p", true)}
    </div>
    
    <div class="subsection">
      <h4 class="subsection-header">Binomial Random Variables</h4>

      <p>A Binomial random variable represents the number of successes
      in {@html katexify("n", false)} independent Bernoulli trials, each with a success probability 
      {@html katexify("p", false)}.</p>

      <p>Let {@html katexify("X", false)} be a Binomial random variable. Then, we write 
      {@html katexify("X\\sim \\text{Bin}(n,p)", false)}. Its pmf is given by:</p>

      {@html katexify("\\mathbb{P}(X=k)={n\\choose k}p^k(1-p)^{n-k},\\ 0 \\leq k \\leq n", true)}
    </div>

    <div class="subsection">
      <h4 class="subsection-header">Geometric Random Variables</h4>

      <p>A Geometric random variable represents the number of Bernoulli
      trials (with success probabiliy {@html katexify("p", false)}) needed to get the first success.</p>

      <p>Let {@html katexify("X", false)} be a Geometric random variable. Then, we write 
      {@html katexify("X\\sim \\text{Geom}(p)", false)}. Its pmf is given by:</p>

      {@html katexify("\\mathbb{P}(X=k)=p(1-p)^{k-1},\\ 1 \\leq k", true)}
    </div>

    <div class="subsection">
      <h4 class="subsection-header">Poisson Random Variables</h4>

      <p>A Poisson random variable counts the number of times an
      event happens in a fixed period of time. It is defined by the average rate of occurrence, 
      {@html katexify("\\lambda", false)}.</p>

      <p>Let {@html katexify("X", false)} be a Poisson random variable. Then, we write 
      {@html katexify("X\\sim \\text{Poisson}(\\lambda)", false)}. Its pmf is given by:</p>

      {@html katexify("\\mathbb{P}(X=k)=e^{-\\lambda}\\frac{\\lambda^k}{k!},\\ 0 \\leq k", true)}
    </div>
  </div>
</main>

<style>
  @import 'styles.css';
</style>