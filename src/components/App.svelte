<script>
	import katexify from '../katexify';
</script>

<svelte:head>
	<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/katex@0.12.0/dist/katex.min.css" integrity="sha384-AfEj0r4/OFrOo5t7NnNe46zW/tFgW6x/bCJG8FqQCEo3+Aro6EYUG4+cU+KJWu/X" crossorigin="anonymous">
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@4.4.1/dist/css/bootstrap.min.css" integrity="sha384-Vkoo8x4CGsO3+Hhxv8T/Q5PaXtkKtu6ug5TOeNV6gBiFeWPGFN9MuhOf23Q9Ifjh" crossorigin="anonymous">
</svelte:head>

<main>
  <div class="container">
    <h1 class="header">Probability & Statistics for Machine Learning</h1>

    <p>What's everyone's least favorite part of machine learning? ... the math! This website
    is an interactive resource that explains probability and statistics concepts that are
    highly prevalent in machine learning.</p>

    <p>By: <a href="https://www.linkedin.com/in/anishkasam/" target="blank">Anish Kasam</a> & 
    <a href="https://www.linkedin.com/in/rushil-c/" target="blank">Rushil Chandrupatla</a></p>

    <div id="prob-spaces" class="section">
      <h2 class="section-header">Probability Spaces & Random Variables</h2>

      <div class="subsection">
        <h4 class="subsection-header">Probability Spaces</h4>

        <p>A probability space can be expressed as a combination of a sample
        space {@html katexify("\\Omega", false)}, collection of events 
        {@html katexify("\\mathcal{F}", false)}, and a probability 
        measure {@html katexify("\\mathbb{P}", false)}.</p>

        <p>A sample space is the collection of all possible outcomes; sample spaces can be either
        discrete or continuous.</p>

        <p><b>Discrete Sample Space:</b> a discrete sample space consists of a finite or countably infinite
        set of distinct outcomes.</p>

        <p><b>Continuous Sample Space:</b> a continuous sample space consists of an uncountably 
        infinite set of outcomes, typically corresponding to all possible values within a certain
        interval.</p>
        
        <p> A collection of events is a subset of the possible outcomes. Finally, 
        a probability measure is a function {@html katexify("\\mathcal{F}\\rightarrow[0,1]", false)}
        that satisfies the following axioms:</p>
        

        <ol>
          <li>{@html katexify("0 \\leq \\mathbb{P}(A) \\leq 1", false)} where 
          {@html katexify("A", false)} is an event.</li>
          <li>{@html katexify("\\mathbb{P}(\\varnothing)=0,\\ \\mathbb{P}(\\Omega)=1", false)}
          ({@html katexify("\\varnothing", false)} denotes the empty set).</li>
          <li>If {@html katexify("A_1,...A_n", false)} are a disjoint sequence of events, then 
          {@html katexify("\\mathbb{P}(A_1\\cup...\\cup A_n)=\\sum^n_{i=1}\\mathbb{P}(A_i)", false)}.</li>
        </ol>

        <p><b>Note:</b> two events are disjoint if their intersection is the empty set.</p>

        <p><b>Inclusion-Exclusion Principle:</b>
        For any two events {@html katexify("A", false)} and {@html katexify("B", false)} in a 
        probability space, 
        {@html katexify("\\mathbb{P}(A\\cup B)=\\mathbb{P}(A)+\\mathbb{P}(B)-\\mathbb{P}(A\\cap B)", false)}.</p>
      </div>

      <div class="subsection">
        <h4 class="subsection-header">Random Variables</h4>

        <p>A random variable is a function {@html katexify("X", false)}: 
        {@html katexify("\\Omega\\rightarrow\\R", false)} where {@html katexify("\\Omega", false)}
        is the sample space of some probability space. A random variable can be either discrete
        (having a specific set of values) or continuous (having any value in a specific range).</p>
      </div>
    </div>

    <div id="prob" class="section">
      <h2 class="section-header">Conditional Probability & Independence</h2>

      <div class="subsection">
        <h4 class="subsection-header">Conditional Probability</h4>

        <p>
        Given a probability space {@html katexify("(\\Omega,\\mathcal{F},\\mathbb{P})", false)}
        and a positive probability event {@html katexify("B\\in\\mathcal{F}", false)}, we can
        define a new probability measure {@html katexify("\\mathbb{P}(-|B)", false)}
        on ({@html katexify("\\Omega,\\mathcal{F}", false)}) defined by:
        </p>

        {@html katexify("\\mathbb{P}(A|B)=\\frac{\\mathbb{P}(A\\cup B)}{\\mathbb{P}(B)}", true)}

        <p><b>Multiplication Rule:</b> 
        {@html katexify("\\mathbb{P}(A\\cap B)=\\mathbb{P}(A|B)\\mathbb{P}(B)=\\mathbb{P}(B|A)\\mathbb{P}(A)", false)}.</p>

        <p><b>Law of Total Probability:</b> if {@html katexify("B_1,B_2,... \\in \\mathcal{F}", false)}
        is a finite or infinite sequence of events partitioning {@html katexify("\\Omega", false)}, then
        for any event {@html katexify("A\\in\\mathcal{F}", false)}: 
        {@html katexify("\\mathbb{P}(A)=\\sum_i\\mathbb{P}(A\\cap B_i)=\\sum_i\\mathbb{P}(A|B_i)\\mathbb{P}(B_i)", false)}.</p>
      </div>

      <div class="subsection">
        <h4 class="subsection-header">Bayes' Theorem</h4>

        {@html katexify("\\mathbb{P}(A|B)=\\frac{\\mathbb{P}(B|A)\\mathbb{P}(A)}{\\mathbb{P}(B)}", true)}
      </div>
      
      <h4 class="subsection-header">Independence</h4>

      <p>Two events {@html katexify("A", false)} and {@html katexify("B", false)} in a probability
      space are independent if any of the three equivalent conditions hold:</p>

      <ol>
        <li>{@html katexify("\\mathbb{P}(A|B)=\\mathbb{P}(A)", false)}.</li>
        <li>{@html katexify("\\mathbb{P}(B|A)=\\mathbb{P}(B)", false)}.</li>
        <li>{@html katexify("\\mathbb{P}(A\\cap B)=\\mathbb{P}(A)\\mathbb{P}(B)", false)}.</li>
      </ol>

      <p><b>Mutual Independence:</b> a sequence of events {@html katexify("A_1,A_2,...", false)} 
      in a probability space are mutually independent if any collection of events
      {@html katexify("A_{i_1},A_{i_2},...,A_{i_n}", false)} chosen from {@html katexify("A_1,A_2,...", false)}
      satisfy {@html katexify("\\mathbb{P}(A_{i_1}\\cap A_{i_2}\\cap...\\cap A_{i_n})=\\mathbb{P}(A_{i_1})\\mathbb{P}(A_{i_2})...\\mathbb{P}(A_{i_n})", false)}.</p>
    </div>

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
        {@html katexify("Y", false)} are random variables defined on the same probability space
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

        {@html katexify("\\text{Var}\\text{(X)}=\\mathbb{E}[(X-\\mu)^2]=\\mathbb{E}[(X-\\mathbb{E}\\text{[X]})^2]=\\mathbb{E}[X^2]-(\\mathbb{E}\\text{[X]})^2", true)}
      
        <p>The standard deviation of {@html katexify("X", false)} is: {@html katexify("\\sqrt{\\text{Var}(X)}", false)}.</p>
      </div>
    </div>

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

    <div id="conf-intervals" class="section">
      <h2 class="section-header">Confidence Intervals</h2>
    </div>

    <div id="sampling" class="section">
      <h2 class="section-header">Sampling</h2>

      <div class="subsection">
        <h4 class="subsection-header">Simple</h4>
      </div>

      <div class="subsection">
        <h4 class="subsection-header">Stratified</h4>
      </div>

      <div class="subsection">
        <h4 class="subsection-header">Clustered</h4>
      </div>
    </div>
  </div>
</main>


<style>
  @import url('https://fonts.googleapis.com/css2?family=Inter:wght@100..900&display=swap');

  .container {
    align-content: left;
    width: 80vw;
    max-width: 800px;
    horizontal-align: middle;
    margin-top: 10vh;
    font-family: Inter;
  }

  .section {
    margin-top: 4vh;
  }

  .subsection {
    margin-top: 2.5vh;
  }

  .subsection-header {
    margin-bottom: 1.5vh;
  }

  .header {
    margin-bottom: 2.5vh;
  }

  b {
    font-weight: 600;
  }

  a {
    color: #1289A7;
    text-decoration: underline;
  }

  a:hover {
    color: #1289A7;
  }
</style>