<svelte:head>
	<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/katex@0.12.0/dist/katex.min.css" integrity="sha384-AfEj0r4/OFrOo5t7NnNe46zW/tFgW6x/bCJG8FqQCEo3+Aro6EYUG4+cU+KJWu/X" crossorigin="anonymous">
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@4.4.1/dist/css/bootstrap.min.css" integrity="sha384-Vkoo8x4CGsO3+Hhxv8T/Q5PaXtkKtu6ug5TOeNV6gBiFeWPGFN9MuhOf23Q9Ifjh" crossorigin="anonymous">
</svelte:head>

<script>
  import katexify from '../katexify';
</script>

<main>
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
      for any two events {@html katexify("A", false)} and {@html katexify("B", false)} in a 
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
</main>

<style>
  @import 'styles.css';
</style>