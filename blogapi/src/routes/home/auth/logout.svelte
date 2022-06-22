<script>
  import axiosInstance from "../../../utils/axios"


  const response = axiosInstance.post('user/logout/blacklist/', {
			refresh_token: localStorage.getItem('refresh_token'),
		});
		localStorage.removeItem('access_token');
		localStorage.removeItem('refresh_token');
		axiosInstance.defaults.headers['Authorization'] = null;
		{window.location.replace("http://127.0.0.1:3000/home")}
	
</script>