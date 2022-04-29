<script>
	import axios from 'axios'
	import { Router, Route, Link } from "svelte-navigator";
	import Login from "./Login.svelte";
	import PrivateRoute from "./PrivateRoute.svelte";
	import { user } from "./store";
	import YouTube from 'svelte-youtube';
	import Swal from 'sweetalert2'
  
  
	function handleLogout() {
	  $user = null;
	}

	function print() {
		axios.get('https://pokeapi.co/api/v2/pokemon/ditto?limit=10').then(
			(response)=>{
				console.log(response.data);
			}
		)
	}

	function evento(e){
		console.log(e);
		Swal.fire(
			{
				title: 'Done',
				icon: 'success'
			}
		)
	}



  </script>
  
  <YouTube
	videoId='vK7JT3nUmFg'                 
	on:end={evento}  
  />
  <Router>
	<header>
	  <h1>History</h1>
  
	  <nav>
		<Link to="/">Home</Link>
		<Link to="about">About</Link>
		<Link to="profile">Profile</Link>
	  </nav>
	</header>
  
	<main>
		<button on:click={print}>

		</button>
	  <Route path="login">
		<Login />
	  </Route>
  
	  <Route path="/">
		<h3>Home</h3>
		<p>Home sweet home...</p>
	  </Route>
  
	  <Route path="about">
		<h3>About</h3>
		<p>That's what it's all about!</p>
	  </Route>
  
	  <PrivateRoute path="profile" let:location>
		<h3>Welcome {$user.username}</h3>
		<button on:click={handleLogout}>Logout</button>
	  </PrivateRoute>
	</main>
  </Router>