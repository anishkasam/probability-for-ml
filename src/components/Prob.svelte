<svelte:head>
	<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/katex@0.12.0/dist/katex.min.css" integrity="sha384-AfEj0r4/OFrOo5t7NnNe46zW/tFgW6x/bCJG8FqQCEo3+Aro6EYUG4+cU+KJWu/X" crossorigin="anonymous">
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@4.4.1/dist/css/bootstrap.min.css" integrity="sha384-Vkoo8x4CGsO3+Hhxv8T/Q5PaXtkKtu6ug5TOeNV6gBiFeWPGFN9MuhOf23Q9Ifjh" crossorigin="anonymous">
</svelte:head>

<script>
  import katexify from '../katexify';
</script>

<main>
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
</main>

<style>
  @import 'styles.css';
</style>