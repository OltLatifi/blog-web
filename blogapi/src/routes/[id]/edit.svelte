<script>
  import axiosInstance from "../../utils/axios"
  import jwt_decode from "jwt-decode";
  // prej context="module"
  export let data;

  
  let token = localStorage.getItem('access_token')
  let decoded = jwt_decode(token)

  let title=data.title
  let excerpt=data.excerpt
  let content=data.content
  let status=data.status
  let category=data.category
  // turns Olt Latifi into olt-latifi
  $: newSlug = title.replace(/\s+/g, '-').toLowerCase();

  const URL = "http://localhost:8000/api/categories/"
  async function getCategories() {
    const res = await fetch(URL);
    const data = await res.json();

		if (res.ok) {
			return data;
		} else {
			throw new Error(data);
		}
	}

  let promise = getCategories();
  

  const Submit =(slug, published)=>{
    axiosInstance.put(`edit/${slug}/`, {
      category: category,
      title: title,
      author: decoded.user_id,
      excerpt: excerpt,
      content: content,
      status: status,
      slug: newSlug,
      published: published
    })
    .then(result=>window.location.replace("/"))

  }
</script>

<script context="module">

  export async function load({fetch, params}) {
    const slug = params.id;
    const response = await axiosInstance.get(`edit/${slug}/`)
    const data = await response.data
    if(response.status===200) {
      return{
        props:{
          data
        }
      }
    }
    return{
        status: response.status,
        error: new Error("Could not fetch our API")
    }
  }
</script>

<div class="center">
  <div class="container">
    <h1>Update</h1>
    <div class="margin-m">
      <label for="title">Title</label><br>
      <input id="title" name="Title" bind:value={title}>
    </div>

    <div class="margin-m">
      <label for="category">Category</label><br>
      {#await promise}
        <input type="number" id="category" list="categories" name="Categories" bind:value={category}><br>
      {:then data_}
        <select id="category" list="categories" name="Categories" bind:value={category}><br>
          {#each data_ as data}
          <option value={data.id}>{data.name}</option>
          {/each}
        </select>
      {:catch error}
        <input type="number" id="category" list="categories" name="Categories" bind:value={category}><br>
      {/await}
    </div>
    <div class="margin-m">
      <label for="status">Status</label><br>
      <select id="status" list="categories" name="Categories" bind:value={status}><br>
        <option value="published" selected>Published</option>
        <option value="draft">Draft</option>
      </select>
    </div>

    <div class="margin-m">
      <label for="excerpt">Excerpt</label><br>
      <textarea type="password" id="excerpt" name="Excerpt" bind:value={excerpt}></textarea><br>
    </div>

    <div class="margin-m">
      <label for="content">Content</label><br>
      <textarea type="content" id="content" name="Content" bind:value={content}></textarea><br>
    </div>
    
    <div class="margin-m">
      <button class="button" on:click={()=>Submit(data.slug, data.published)}>Submit</button>
    </div>
  </div>
</div>
<br>
<style>
  #content {
    height:150px;
  }
</style>