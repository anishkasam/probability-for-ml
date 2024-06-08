<script>
  import App from '../components/App.svelte';
  import ProbSpaces from '../components/ProbSpaces.svelte';
  import Prob from '../components/Prob.svelte';
  import Distrs from '../components/Distrs.svelte';
  import Drvs from '../components/Drvs.svelte';
  import Crvs from '../components/Crvs.svelte';
  import ExpVar from '../components/ExpVar.svelte';
  import Theorems from '../components/Theorems.svelte';
  import Intro from '../components/Intro.svelte';
  import Hist from '../components/Hist.svelte';
  import Kde from '../components/Kde.svelte';
  import Pde from '../components/Pde.svelte';
  import Sampling from '../components/Sampling.svelte';
  import Appendix from '../components/Appendix.svelte';
  import InPractice from '../components/InPractice.svelte';
</script>

<svelte:head>
	<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/katex@0.12.0/dist/katex.min.css" integrity="sha384-AfEj0r4/OFrOo5t7NnNe46zW/tFgW6x/bCJG8FqQCEo3+Aro6EYUG4+cU+KJWu/X" crossorigin="anonymous">
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@4.4.1/dist/css/bootstrap.min.css" integrity="sha384-Vkoo8x4CGsO3+Hhxv8T/Q5PaXtkKtu6ug5TOeNV6gBiFeWPGFN9MuhOf23Q9Ifjh" crossorigin="anonymous">
</svelte:head>

<main>
  <div class="container">
    <App />
    <Intro />
    <Hist />
    <Kde />
    <Pde />
    <InPractice />
    <Sampling />
    <Appendix />
    <ProbSpaces />
    <Prob />
    <Distrs />
    <Drvs />
    <Crvs />
    <ExpVar />
    <Theorems />
  </div>
</main>

<style>
  .container {
    align-content: left;
    width: 80vw;
    max-width: 800px;
    margin-top: 10vh;
    font-family: Inter;
  }
</style>