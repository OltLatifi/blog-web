<script>

import SmallBlog from "$lib/SmallBlog.svelte";

const URL = "http://localhost:8000/api/"
async function getData() {
		const res = await fetch(URL);
		const data = await res.json();

		if (res.ok) {
			return data;
		} else {
			throw new Error(data);
		}
	}
	
	let promise = getData();
  console.log(promise);

</script>



<slot></slot>

{#await promise}
	<p>...waiting</p>
{:then data_}
  <div class="blog-row">
    {#each data_ as data}
    <!-- {console.log(data)} -->
    <SmallBlog title={data.title} content={data.content} date={data.date}/>
    {/each}
  </div>
{:catch error}
	<p style="color: red">{error.message}</p>
{/await}


<style>
  .blog-row{
    display:flex;
    flex-wrap: wrap;
    margin: 2%;

  }
</style>