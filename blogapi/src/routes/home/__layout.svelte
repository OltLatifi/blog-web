
<script>
  import Header from '$lib/Header.svelte'
  import Footer from '$lib/Footer.svelte'
  import "../../styles/main.css" 
</script>

<body>
  <Header/>
  <slot></slot>
  <Footer/>
</body>
