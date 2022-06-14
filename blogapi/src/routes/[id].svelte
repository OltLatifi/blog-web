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

<div>
  {post.title}
  {post.excerpt}
  {post.content}
  {post.status}
</div>