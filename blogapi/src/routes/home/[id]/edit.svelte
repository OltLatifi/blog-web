<script>
  import axiosInstance from "../../../utils/axios"
  import jwt_decode from "jwt-decode";
  // prej context="module"
  export let data;

  
  let token = localStorage.getItem('access_token')
  let decoded = jwt_decode(token)

  let title=data.title
  let image = data.image
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
  

  const Submit =(slug)=>{
    if(title!==""){
      if(status!==""){
        if(excerpt!==""){
          if(content!==""){
            let data = new FormData();
            data.append('title', title);
            data.append('category', category);
            data.append('status', status);
            data.append('excerpt', excerpt);
            data.append('content', content);
            data.append('slug', newSlug);
            data.append('published', '2022-06-18T13:57:22.732328Z');
            data.append('author', decoded.user_id);
            // if a new image is uploaded
            if(typeof image ==='object') {
              data.append('image', image[0])
            }
            axiosInstance.put(`edit/${slug}/`, data)
            .then(result=>window.location.replace("/home/admin/posts"))
          }else{
            alert("Please enter the blog content")
          }
        }else{
          alert("Please enter an excerpt")
        }
      }else{
        alert("Please select status")
      }
    }else{
      alert("Please enter a title")
    }


  }
</script>

<script context="module">

  export async function load({params}) {
    const slug = params.id;
    const response = await axiosInstance.get(`${slug}/`)
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
      <label for="image-lbl">Image</label><br>
      {#if !image}
        <label for="image-upload" id="image-lbl" class="button">
          Upload image
          <input id="image-upload" type="file" accept="image/*" name="Image" bind:files={image}>
        </label>
      {:else}
        <label for="image-upload" id="image-lbl" class="button">
          Image uploaded
          <input id="image-upload" type="file" accept="image/*" name="Image" bind:files={image}>
        </label>
      {/if}
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
      <button class="button" on:click={()=>Submit(data.slug)}>Submit</button>
    </div>
  </div>
</div>
<br>
<style>
  #image-upload{
    display: none;
  }

  #image-lbl{
    cursor: pointer;
    border: 1px solid black;
    border-radius: 1px;
  }
</style>