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
        <SmallBlog slug={data.slug} title={data.title} excerpt={data.excerpt} image={data.image} date={data.published.split("T")[0]}/>
      {/each}
    </div>
  {:catch error}
    <p style="color: red">{error}</p>
  {/await}
  
  
  