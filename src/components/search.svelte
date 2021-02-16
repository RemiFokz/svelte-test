<script>
  import { createEventDispatcher } from "svelte";

  export let search;
  const dispatch = createEventDispatcher();
</script>

<input
  placeholder="search user"
  class="bg-gray-300 p-3"
  bind:value={search}
  on:input={(e) => dispatch('search', e)}
  type="text" />
