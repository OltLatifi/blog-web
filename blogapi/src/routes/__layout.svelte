
<script>
  import Header from '$lib/Header.svelte'
  import Footer from '$lib/Footer.svelte'
  import "../styles/main.css" 
</script>

<Header/>
<main>
  <slot></slot>
</main>
<Footer/>
