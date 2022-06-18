<script>
  export let title="a title";
  export let content="a content";
  export let date="a date";
  export let slug;
</script>

<div class="small-container">
  <a href={`/${slug}/`}>
  <h3>
    {title}
  </h3>
  <p>{content}</p>
  <span>{date}</span>
  </a>
</div>


<style>
  a{
    text-decoration: none;
    color: black;
  }
  .small-container {
    margin:4px;
    padding:0 12px;
    flex-basis: 12rem;
    /* border: 1px solid black; */
    flex-grow: 1;

    width:20%;
    box-shadow: rgba(0, 0, 0, 0.16) 0px 1px 4px;
    border: 1px solid #ccc;
  }
</style>