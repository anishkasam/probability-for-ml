<svelte:head>
	<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/katex@0.12.0/dist/katex.min.css" integrity="sha384-AfEj0r4/OFrOo5t7NnNe46zW/tFgW6x/bCJG8FqQCEo3+Aro6EYUG4+cU+KJWu/X" crossorigin="anonymous">
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@4.4.1/dist/css/bootstrap.min.css" integrity="sha384-Vkoo8x4CGsO3+Hhxv8T/Q5PaXtkKtu6ug5TOeNV6gBiFeWPGFN9MuhOf23Q9Ifjh" crossorigin="anonymous">
</svelte:head>

<script>
  import katexify from '../katexify';
</script>

<main>
  <div id="prob-distrs" class="section">
    <h2 class="section-header">Probability Distribution Functions</h2>

    <div class="subsection">
      <h4 class="subsection-header">Cumulative Density Functions (CDFs)</h4>
      
      <p>Let {@html katexify("X", false)} be a random variable. The cumulative density
      function (cdf) of {@html katexify("X", false)} is the function 
      {@html katexify("F_x", false)}: {@html katexify("\\R\\rightarrow\\R", false)}
      defined by {@html katexify("F_x(t)=\\mathbb{P}(X\\leq t)=\\mathbb{P}(X\\in(-\\infty ,t])", false)}
      The cdf gives us the probability that {@html katexify("X", false)} is less than or equal to some value.</p>
    
      <p>A function {@html katexify("F", false)}: {@html katexify("\\R\\rightarrow\\R", false)} is the cdf of
      a random variable if and only if:</p>

      <ol>
        <li>{@html katexify("\\lim_{t\\to-\\infty}F(t)=0", false)} and {@html katexify("\\lim_{t\\to\\infty}F(t)=1", false)}</li>
        <li>{@html katexify("F", false)} is nondecreasing: if {@html katexify("s \\leq t", false)} then {@html katexify("F(s) \\leq F(t)", false)}</li>
        <li>{@html katexify("F", false)} is right continuous: {@html katexify("\\lim_{t\\to a^+}F(t)=F(a)", false)}</li>
      </ol>
    </div>

    <div class="subsection">
      <h4 class="subsection-header">Probability Mass Functions (PMFs)</h4>
      
      <p>Let {@html katexify("X", false)} be a discrete random variable. The probability mass
      function (pmf) of {@html katexify("X", false)} is defined as {@html katexify("p_x(a)=\\mathbb{P}(X=a)", false)}.
      The pmf gives us the probability that {@html katexify("X", false)} is exactly equal 
      to some value.</p>

      <p>A function {@html katexify("p", false)}: {@html katexify("\\R\\to\\R", false)} is the pmf of a discrete
      random variable if and only if there exists a finite or infinite sequence of numbers 
      {@html katexify("a_1,a_2,...\\in\\R", false)} such that:</p>

      <ol>
        <li>{@html katexify("0 \\leq p(a_i) \\leq 1", false)} for all {@html katexify("a_i", false)}</li>
        <li>{@html katexify("\\sum_i p(a_i)=1", false)}</li>
        <li>{@html katexify("p(a)=0", false)} if {@html katexify("p\\notin\\{a_1,a_2,...\\}", false)}</li>
      </ol>
    </div>

    <div class="subsection">
      <h4 class="subsection-header">Probability Density Functions (PDFs)</h4>
      
      <p>Let {@html katexify("X", false)} be a continuous random variable. The probability density
      function (pdf) of {@html katexify("X", false)} is defined as {@html katexify("f_x(t)", false)}.
      The pdf gives us the relative likelihood (not a probability) that {@html katexify("X", false)} is exactly equal 
      to some value.</p>

      <p>To find the probability that {@html katexify("X", false)} falls in a certain interval, we can take the
      integral of the pdf over that interval:</p>

      {@html katexify("\\mathbb{P}(X\\in[a,b])=\\int^b_a f_x(t) dt", true)}

      <p>A function {@html katexify("f", false)}: {@html katexify("\\R\\to\\R", false)} is the pdf of a continuous
      random variable if and only if:</p>

      <ol>
        <li>{@html katexify("f", false)} is integrable</li>
        <li>{@html katexify("f(t)\\geq 0", false)} for all {@html katexify("t", false)}</li>
        <li>{@html katexify("\\int^{\\infty}_{-\\infty} f(t) dt=1", false)}</li>
      </ol>
    </div>

    <div class="subsection">
      <h4 class="subsection-header">Converting PMFs/PDFs to CDFs</h4>
      
      <p>If {@html katexify("X", false)} is discrete:</p>
      {@html katexify("F_x(t)=\\mathbb{P}(X\\leq t)=\\sum_{a\\leq t}p_x(a)", true)}

      <p>If {@html katexify("X", false)} is continuous:</p>
      {@html katexify("F_x(t)=\\mathbb{P}(X\\leq t)=\\int^{t}_{-\\infty}f_x(s)ds", true)}
    </div>

    <div class="subsection">
      <h4 class="subsection-header">Converting CDFs to PMFs/PDFs</h4>
      
      <p>Let {@html katexify("X", false)} be a random variable and {@html katexify("F_x", false)} its cdf.</p> 
      
      <p>If {@html katexify("F_x", false)} is piecewise constant, then {@html katexify("X", false)} is 
      discrete and its pmf is found by calculating the magnitude of the jumps at the points of discontinuity.</p>

      <p>If {@html katexify("F_x", false)} is continuous and piecewise continuously differentiable, then
      {@html katexify("X", false)} is continuous and its pdf is given by {@html katexify("f_x(t)=F_x'(t)", false)}</p>
    </div>
  </div>
</main>

<style>
  @import 'styles.css';
</style>