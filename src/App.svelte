<script>
import { Router, Link, Route, navigate } from "svelte-routing"
import Login from "./Login.svelte"
import Somewhere from "./Somewhere.svelte"
import Home from "./Home.svelte"
import { tick } from "svelte"

let user = null
var previousPath

$: user

function logout() {
    localStorage.clear()
    user = null
    navigate("/")
}

async function loggedIn (event) {
    if (event) {
        user = { name: "George" }
        await tick()
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
        <Route path="/login"><Login on:loggedIn={loggedIn} path={previousPath} /></Route>
        {/if}
    </main>
</Router>
