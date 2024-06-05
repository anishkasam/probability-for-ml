<svelte:head>
	<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/katex@0.12.0/dist/katex.min.css" integrity="sha384-AfEj0r4/OFrOo5t7NnNe46zW/tFgW6x/bCJG8FqQCEo3+Aro6EYUG4+cU+KJWu/X" crossorigin="anonymous">
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@4.4.1/dist/css/bootstrap.min.css" integrity="sha384-Vkoo8x4CGsO3+Hhxv8T/Q5PaXtkKtu6ug5TOeNV6gBiFeWPGFN9MuhOf23Q9Ifjh" crossorigin="anonymous">
</svelte:head>

<script>
  import katexify from '../katexify';
</script>

<main>
  <div class="subsection">
    <h4 class="subsection-header">Gaussian Kernel Density Estimators (KDE)</h4>

    <p>Gaussian kernel density estimators are another intuitive density
    estimation technique. The main idea is to place a kernel function, 
    in this case a normalized Gaussian, at every data point. The sum of all 
    of these Gaussians will resulting in a valid density function that is 
    more appealing than the one derived using a histogram estimator.</p>

    <p>The kernel function is a Gaussian with a mean of {@html katexify("0", false)}
    and a variance of {@html katexify("1", false)}; its pdf is given by:</p>

    {@html katexify("K(x)=\\frac{1}{\\sqrt{2\\pi}}e^\\frac{-x^2}{2}", true)}

    <p>The overall density function is given by:</p>

    {@html katexify("f(x)=\\frac{1}{nh}\\sum^n_{i=1}K(\\frac{x-x_i}{h})", true)}

    <p>In this equation, {@html katexify("\\frac{1}{n}", false)} ensures that
    the sum of all {@html katexify("n", false)} Gaussians is normalized,
    mainting an area of {@html katexify("1", false)}. Additionally, 
    {@html katexify("h" , false)} controls the width of each Gaussian.</p>
    </div>
</main>

<style>
  @import 'styles.css';
</style>