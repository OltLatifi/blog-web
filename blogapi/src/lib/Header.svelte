
<script>
  import axiosInstance from "../utils/axios"
</script>
{#if axiosInstance.defaults.headers['Authorization'] !== null}
<nav class="navbar">
  <div class="left">
    <h1><a href="/home">Home</a></h1>
  </div>
  <div class="navbar-right">
    <ul class="right">
      <li class="right-child"><a href="/home/admin/posts">Admin</a></li>
      <li class="right-child"><a href="/home/create">Create</a></li>
      <li class="right-child"><a href="/home/filter">Filter</a></li>
      <li class="right-child"><a href="/home/auth/register">Register</a></li>
      <li class="right-child"><a href="/home/auth/logout">Logout</a></li>

    </ul>
  </div>
</nav>
{:else}
<nav class="navbar">
  <div class="left">
    <h1><a href="/home">Home</a></h1>
  </div>
  <div class="navbar-right">
    <ul class="right">
      <li class="right-child"><a href="/home/filter">Filter</a></li>
      <li class="right-child"><a href="/home/auth/register">Register</a></li>
      <li class="right-child"><a href="/home/auth/login">Login</a></li>

    </ul>
  </div>
</nav>

{/if}

