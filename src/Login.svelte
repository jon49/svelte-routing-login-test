<script>
import { createEventDispatcher } from "svelte";

const dispatch = createEventDispatcher()

function submit() {
    dispatch("loggedIn", true)
}
</script>

<form on:submit={submit}>
    <input type="submit" value="Submit" />
</form>

