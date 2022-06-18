<script>
  import axiosInstance from "../utils/axios"
  import jwt_decode from "jwt-decode";
  
  let token = localStorage.getItem('access_token')
  let decoded = jwt_decode(token)

  let title=""
  let excerpt=""
  let content=""
  let status=""
  let category;
  // turns Olt Latifi into olt-latifi
  $: slug = title.replace(/\s+/g, '-').toLowerCase();

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

  const Submit =()=>{
    console.log(category)
    // })
    axiosInstance.post('create/', {
      category: category,
      title: title,
      author: decoded.user_id,
      excerpt: excerpt,
      content: content,
      status: status,
      slug: slug,
      published:"2022-06-18T15:10:25.355111Z"
    })
    .then(result=>window.location.replace("/"))

  }
</script>

<div class="center">
  <div class="container">
    <h1>Create</h1>
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
          {console.log(`${data.id} | ${data.name}`)}
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
      <button class="button" on:click={Submit}>Submit</button>
    </div>
  </div>
</div>
<br>
<style>
  #content {
    height:150px;
  }
</style>