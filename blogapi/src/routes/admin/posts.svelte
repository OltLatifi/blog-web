<script>
  import axiosInstance from "../../utils/axios"
  
  const URL = "http://localhost:8000/api/edit/postdetail/"
  async function getData() {
    const res = await axiosInstance.get(URL)
    const data = await res.data
    return data;

	}
	
	let promise = getData();
</script>

<div class="container dimensions">

  {#await promise}
    <p>...waiting</p>
  {:then data_}
    {#if data_.length==0}
      <h2>Here you can view and modify your posts once you make them.</h2>
    {/if}
    <table>
      <tr>
        <th>Title</th>
        <th>Date</th>
        <th>Status</th>
        <th>Actions</th>
      </tr>
      
      {#each data_ as data}
      <tr>
        <td>
          <a href={`/${data.title}/`}>
            {data.title}
          </a>
        </td>
        <td>{data.date.split("T")[0]}</td>
        <!-- capitalises -->
        <td>{data.status.charAt(0).toUpperCase() + data.status.slice(1)}</td>
        <td><button class="button edit" title="Edit">✎</button> <button class="button delete" title="Delete">&#x1F5D1</button>
          <!-- if the post is a draft ad an option to publish -->
          {#if data.status.charAt(0).toUpperCase()==="D"}
            <button class="button publish" title="Publish">☑</button>
          {/if}
        </td>
      </tr>
      {/each}
  
      
    </table>
  {:catch error}
    {window.location.replace("http://127.0.0.1:3000/admin/redirect")}
  {/await}
</div>





<style>
  table {
    border-collapse: collapse;
    width:100%;
  }

  .dimensions{
    width: 80%;
    margin: 5% 10%;
  }
  
  td, th {
    border: 1px solid black;
    text-align: left;
    padding: 8px;
    width:20%;

  }

  a{
    text-decoration: none;
    color: black;
  }
  
  td:nth-child(1), th:nth-child(1) {
    width:40%;
  }

  button{
    width:50px;
    margin: 2px 0;
  }
  .edit{
    border: 1px solid blue;
    color: blue;
  }

  .delete{
    border: 1px solid rgb(193, 69, 69);
    color: rgb(193, 69, 69);
  }

  .publish{
    border: 1px solid green;
    color: green;
  }
</style>