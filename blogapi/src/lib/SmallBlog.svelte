<script>
  export let title="a title";
  export let excerpt;
  export let date;
  export let image;
  export let slug;
</script>

<div class="small-container">
  <img src={image} alt="Blog related" loading="lazy">
  <a href={`/home/${slug}/`}>
  <h3>
    {title}
  </h3>
  <p>{excerpt}</p>
  <p>{date}</p>
  </a>
</div>


<style>
  a{
    text-decoration: none;
    color: black;
  }

  h3, p{
    padding:8px;
  }
  
  .small-container {
    margin:1%;
    /* padding:0 12px; */
    flex-basis: 18rem;
    flex-grow: 1;
    flex-shrink: 0;
    max-width:98%;

    display:flex;
    flex-direction: row;
    box-shadow: rgba(0, 0, 0, 0.16) 1px 2px 6px;
  }

  @media only screen and (min-width: 650px) {
    /* big screen */
    .small-container {
    margin:0.5%;
    flex-basis: 24rem;
    flex-grow: 1;
    flex-shrink: 0;
    max-width:49%;

    display:flex;
    flex-direction: row;
    box-shadow: rgba(0, 0, 0, 0.16) 1px 2px 6px;
  }
  }

  img{
    aspect-ratio: 1 / 1;
    min-width:46%;
    max-width: 46%;
    margin: 2%;
    overflow: hidden;
    object-fit: cover;
    /* filter:grayscale(1); */
  }
</style>