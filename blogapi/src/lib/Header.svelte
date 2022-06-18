
<script>
  import axiosInstance from "../utils/axios"
</script>
{#if axiosInstance.defaults.headers['Authorization'] !== null}
<ul class="topnav">
  <li><a class="active" href="/">Home</a></li>
  <li><a href="/admin/posts">Admin</a></li>
  <li><a href="/create">Create</a></li>
  <li><a href="/filter">Filter</a></li>
  <li><a href="/auth/register">Register</a></li>
  <li class="right"><a href="/auth/logout">Logout</a></li>
</ul>
{:else}
<ul class="topnav">
  <li><a class="active" href="/">Home</a></li>
  <li><a href="/filter">Filter</a></li>
  <li><a href="/auth/register">Register</a></li>
  <li class="right"><a href="/auth/login">Login</a></li>
</ul>

{/if}
