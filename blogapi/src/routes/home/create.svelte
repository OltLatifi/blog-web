<script>
  import { quill } from 'svelte-quill'
  import axiosInstance from "../../utils/axios"
  import jwt_decode from "jwt-decode";
  
	let options = { placeholder: "Write something from outside...", }
  let token = localStorage.getItem('access_token')
  let decoded = jwt_decode(token)

  let title=""
  let excerpt=""
  let status=""
  let category;
  let image;

	let content = { html: '', text: ''};

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

    if(title!==""){
      if(status!==""){
        if(excerpt!==""){
          if(content.html!==""){
            if(image){
              axiosInstance.post('create/', {
              category: category,
              title: title,
              author: decoded.user_id,
              image: image[0],
              excerpt: excerpt,
              content: content.html,
              status: status,
              slug: slug,
              published:"2022-06-18T15:10:25.355111Z"
            })
            .then(result=>window.location.replace("/home"))
            } else{
              axiosInstance.post('create/', {
              category: category,
              title: title,
              author: decoded.user_id,
              excerpt: excerpt,
              content: content.html,
              status: status,
              slug: slug,
              published:"2022-06-18T15:10:25.355111Z"
            })
            .then(result=>window.location.replace("/home"))
            }
            

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

<svelte:head>
	<link href="//cdn.quilljs.com/1.3.6/quill.snow.css" rel="stylesheet">
</svelte:head>

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
          {image[0].name}
          <input id="image-upload" type="file" accept="image/*" name="Image" bind:files={image}>
        </label>
      {/if}
    </div>

    <div class="margin-m">
      <label for="excerpt">Excerpt</label><br>
      <textarea type="password" id="excerpt" name="Excerpt" maxlength="10000" bind:value={excerpt}></textarea><br>
    </div>

    <div class="margin-m">
      <label for="content">Content</label><br>
      <div class="quill-container">
        <div class="quill" use:quill={options} on:text-change={e => content = e.detail}/>
      </div>
      <!-- <textarea type="content" id="content" name="Content" bind:value={content}></textarea><br> -->
    </div>
    
    <div class="margin-m">
      <button class="button" on:click={Submit}>Submit</button>
    </div>
  </div>
</div>
<br>
<style>
  .quill-container{
    width:80%;
    margin:0 10%;
    /* resize: vertical; */
    border: 1px solid black;
    border-radius: 1px;
  }

  .quill{
    width:100%;
  }
  #image-upload{
    display: none;
  }

  #image-lbl{
    cursor: pointer;
    border: 1px solid black;
    border-radius: 1px;
  }
</style>