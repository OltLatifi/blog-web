<script>
  import axiosInstance from "../../utils/axios"

  let email="";
  let password="";
  

  const LogIn =()=>{
    axiosInstance.post('token/', {
      email: email,
      password: password,
    })
    .then(result=>{
      localStorage.setItem('access_token', result.data.access);
      localStorage.setItem('refresh_token', result.data.refresh);

      axiosInstance.defaults.headers['Authorization'] =
        'Bearer ' + localStorage.getItem('access_token');
  })
    .then(result=>window.location.replace("http://127.0.0.1:3000/"))

  }
</script>

<div class="center">
  <div class="container">
    <h1>Log in</h1>
    <div class="margin-m">
      <label for="email">Email</label><br>
      <input type="email" id="email" name="Email" bind:value={email}>
    </div>
    <div class="margin-m">
      <label for="password">Password</label><br>
      <input type="password" id="password" name="Password" bind:value={password}><br>
    </div><br>

    <button class="button" on:click={LogIn}>Login</button>
  </div>
</div>
