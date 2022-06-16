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

</script>


{#await promise}
	<p>...waiting</p>
{:then data_}
  <div class="blog-row">
    {#each data_ as data}
    <!-- {console.log(data)} -->
    <SmallBlog title={data.title} content={data.content} date={data.date.split("T")[0]}/>
    {/each}
  </div>
{:catch error}
	<p style="color: red">{error}</p>
{/await}


