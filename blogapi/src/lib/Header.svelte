
<script>
  import axiosInstance from "../utils/axios"
</script>
{#if axiosInstance.defaults.headers['Authorization'] !== null}
<ul class="topnav">
  <li><a class="active" href="/home">Home</a></li>
  <li><a href="/home/admin/posts">Admin</a></li>
  <li><a href="/home/create">Create</a></li>
  <li><a href="/home/filter">Filter</a></li>
  <li><a href="/home/auth/register">Register</a></li>
  <li class="right"><a href="/home/auth/logout">Logout</a></li>
</ul>
{:else}
<ul class="topnav">
  <li><a class="active" href="/home">Home</a></li>
  <li><a href="/home/filter">Filter</a></li>
  <li><a href="/home/auth/register">Register</a></li>
  <li class="right"><a href="/home/auth/login">Login</a></li>
</ul>

{/if}
