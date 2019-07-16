<script>
import { Router, Link, Route, navigate } from "svelte-routing"
import Login from "./Login.svelte"
import Somewhere from "./Somewhere.svelte"
import Home from "./Home.svelte"

let user = null
var previousPath

$: user

function logout() {
	localStorage.clear()
	user = null
	navigate("/")
}

function loggedIn (event) {
	if (event) {
		user = { name: "George" }
		navigate(previousPath, { replace: true })
	}
}

function loggingIn() {
	previousPath = window.location.pathname
}

</script>

<Router>
	<h1>Test Login</h1>
	<nav>
		<Link to="/">Home</Link>
		{#if user === null}
		<Link to="/login" on:click={loggingIn}>Login</Link>
		{:else}
		<Link to="/somewhere">Somewhere</Link>
		<form on:submit={logout}>
			<input type="submit" value="Logout" />
		</form>
		{/if}
	</nav>
	<main>
		{#if user !== null}
		<Route path="/somewhere"><Somewhere /></Route>
		<Route path="/"><Home /></Route>
		{:else}
		<p>Please login</p>
		<Route path="/login"><Login on:loggedIn={loggedIn} /></Route>
		{/if}
	</main>
</Router>
