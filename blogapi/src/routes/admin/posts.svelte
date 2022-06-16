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

{#await promise}
  <p>...waiting</p>
{:then data_}
  <table>
    <tr>
      <th>Title</th>
      <th>Date</th>
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
      <td><button class="button">✎</button> <button class="button">&#x1F5D1</button></td>
    </tr>
    {/each}

    
  </table>
{:catch error}
  <h1>To access the admin page you need to login first.</h1>
{/await}





<style>
  table {
    border-collapse: collapse;
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
    width:60%;
  }
</style>