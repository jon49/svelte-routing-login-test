<script>
import { createEventDispatcher, onDestroy } from "svelte";
import { navigate } from "svelte-routing"

export let path
console.log("path:", path)

const dispatch = createEventDispatcher()

function submit() {
    dispatch("loggedIn", true)
}
</script>

<form on:submit={submit}>
    <input type="submit" value="Submit" />
</form>

