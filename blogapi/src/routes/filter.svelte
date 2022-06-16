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


{#if filtered}
<div>
  <div class="blog-row">
    {#each blogPost as data}
    <SmallBlog title={data.title} content={data.content} date={data.date.split("T")[0]}/>
    {/each}
  </div>
</div>
{/if}


<style>
  h1, input, label, button, select{
    width:80%;
    margin-left:10%;
  }
  
</style>