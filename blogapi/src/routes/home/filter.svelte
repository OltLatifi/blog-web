<script>
  
  import SmallBlog from "$lib/SmallBlog.svelte";
  const URL = "http://localhost:8000/api/categories/"
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
  let title="";
  let category="";
  let blogPost=[];
  let filtered = false;



  async function filter(){
    let baseURL = "http://127.0.0.1:8000/api/"
    let isUsed = false
    filtered = false

    if(category!==''){
      if(!isUsed){
        baseURL+=`?category=${category}`
        isUsed = true;
      }
      baseURL+=`&category=${category}`
    }
    if(title!==''){
      if(!isUsed){
        baseURL+=`?title=${title}`
        isUsed = true;
      }
      baseURL+=`&title=${title}`
    }
    const res = await fetch(baseURL);
    const data = await res.json();

		if (res.ok) {
			blogPost = data
      filtered= true;

		} else {
			throw new Error(data);
		}
  }


</script>

{#if !filtered}

<div class="center">
  <div class="container">
    <h1>Filter</h1>
    <div class="margin-m">
      <label for="title">Title:</label><br>
      <input id="title" name="Title" bind:value={title}><br>
    </div>
    <div class="margin-m">
      <label for="category">Category:</label><br>
      {#await promise}
      <input id="category" list="categories" name="Categories" bind:value={category}><br>
      {:then data_}
        <select id="category" list="categories" name="Categories" bind:value={category}><br>
          {#each data_ as data}
            <option value={data.id}>{data.name}</option>
          {/each}
        </select>
      {:catch error}
        <p style="color: red">{error}</p>
      {/await}
    </div>
    <br>
    <button class="button" on:click={filter}>Filter</button>
  
  
  </div>
</div>

{:else}


<div>
  <button id="filter-again" class="button" on:click={()=>filtered=false}>Filter again.</button>
  <div class="blog-row">
    {#each blogPost as data}
    <SmallBlog slug={data.slug} title={data.title} excerpt={data.excerpt} image={data.image} date={data.published.split("T")[0]}/>
    {/each}
  </div>
</div>

{/if}


<style>
  #filter-again{
    width:50%;
    margin-top: 3%;
    margin-bottom: 0;
    margin-left: 3%;
  }
</style>