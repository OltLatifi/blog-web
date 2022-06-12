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

      let obj={
        Authorization:`Bearer ${localStorage.getItem('access_token')}`
      }
      // add authorization to the headers
      axiosInstance.defaults.headers=Object.assign(axiosInstance.defaults.headers, obj)
  })
    .then(result=>window.location.replace("http://127.0.0.1:3000/"))

  }
</script>


<div style="margin-left:2%;">
  <label for="email">Email:</label><br>
  <input type="email" id="email" name="Email" bind:value={email}><br>

  <label for="password">Password</label><br>
  <input type="password" id="password" name="Password" bind:value={password}><br><br>

  <button on:click={LogIn}>Login</button>
</div>