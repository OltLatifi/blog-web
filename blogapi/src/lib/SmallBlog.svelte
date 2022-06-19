<script>
  export let title="a title";
  export let excerpt="an excerpt";
  export let date="a date";
  export let image;
  export let slug;
</script>

<div class="small-container">
  <img src={image} alt="Blog related">
  <a href={`/${slug}/`}>
  <h3>
    {title}
  </h3>
  <p>{excerpt}</p>
  <span>{date}</span>
  </a>
</div>


<style>
  a{
    text-decoration: none;
    color: black;
  }
  
  .small-container {
    margin:1%;
    /* padding:0 12px; */
    flex-basis: 18rem;
    border: 1px solid black;
    flex-grow: 1;
    flex-shrink: 0;
    max-width:98%;

    display:flex;
    flex-direction: row;
    box-shadow: rgba(0, 0, 0, 0.16) 0px 1px 4px;
  }

  @media only screen and (min-width: 650px) {
    /* big screen */
    .small-container {
    margin:0.5%;
    flex-basis: 18rem;
    border: 1px solid black;
    flex-grow: 1;
    flex-shrink: 0;
    max-width:49%;

    display:flex;
    flex-direction: row;
    box-shadow: rgba(0, 0, 0, 0.16) 0px 1px 4px;
  }
  }

  img{
    aspect-ratio: 1 / 1;
    width:50%;
    max-width: 11rem;
    overflow: hidden;
  }
</style>