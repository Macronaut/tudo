<script>
	import { Router, Link, Route } from "svelte-routing";
	import Login from "./routes/Login.svelte";
	import List from "./routes/List.svelte";

  	export let url = "";

	Parse.serverURL = 'https://parseapi.back4app.com';
	Parse.initialize('rkwXxU6sEJx1oCm1xh9U8XcJ7q5B9hyru3s0Z8LY', 'ItgUzDXip0Aujpbo1Vjf6c3hBjUTaQQ5BCesmTnw');
</script>

<style>
  .component-app { margin-top: 20px }
</style>

<Router url="{url}">
  <!-- <nav>
    <Link to="/">Home</Link>
    <Link to="about">About</Link>
    <Link to="blog">Blog</Link>
  </nav> -->
  <div class="component-app">
    <Route path="list" component="{List}" />
    <Route path="/"><Login /></Route>
  </div>
</Router>