<script>
  import axiosInstance from "../../utils/axios"

  let email_="";
  let username="";
  let password="";
  let data;

  /**
* @param {string} email
*/
  function validateEmail(email) 
    {
      let re = /\S+@\S+\.\S+/;
      return re.test(email);
    }
    
  const signUp =()=>{
    if(validateEmail(email_)){ 
      if(username.split("").length >=1){
        if(password.split("").length >= 8){
          axiosInstance.post('/user/register/', {
          email: email_,
          user_name: username,
          password: password,
          })
          .then(result=>console.log(result.status))
          .then(result=>window.location.replace("http://127.0.0.1:3000/auth/login/"))
          .catch(error => {
            if(error.response.status ===400){
              alert("Your email and username should be unique. They are already taken.")
            }
          })
        }
        else{
          alert("Please enter a password with at least 8 characters.");
        }
      }
      else{
        alert("Please enter a username.")
      }
    }else{
      alert("Please enter a valid email address.")
    }
    


  }
</script>


<div style="margin-left:2%;">
  <label for="email">Email:</label><br>
  <input type="email" id="email" name="Email" required bind:value={email_}
  ><br>

  <label for="username">Username</label><br>
  <input type="text" id="username" name="Username" required bind:value={username}><br>

  <label for="password">Password</label><br>
  <input type="password" id="password" name="Password" required bind:value={password}><br><br>

  <button on:click={signUp}>Register</button>
</div>