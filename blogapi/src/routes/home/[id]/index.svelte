<script context="module">
  export async function load({fetch, params}) {
    const slug = params.id;
    const response = await fetch(`http://127.0.0.1:8000/api/${slug}/`)
    const post = await response.json()
    if(response.ok) {
      return{
        props:{
          post
        }
      }
    }
    return{
        status: response.status,
        error: new Error("Could not fetch our API")
    }
  }
</script>
<script>
  export let post;
</script>

<div class="container detailview">
  <div class="content">
    <img src={post.image} alt="Blog related">
    <h1>{post.title}</h1>
    {@html post.content}
  </div>
</div>


<style>
  .detailview {
    width: 90%;
    display: flex;
    flex-direction: column;
    margin:2%;
  }
  .content{
    width:70%;
    margin:0 15%;
  }
  img{
    aspect-ratio:16/9;
    width:100%;
  }
  h1{
    margin:0;
    font-size:2.5em;
  }
</style>