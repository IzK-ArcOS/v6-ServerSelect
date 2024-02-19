<script lang="ts">
  import { setServer } from "$ts/server/multi";
  import { PrimaryState } from "$ts/states";
  import { ServerSelectOption } from "$types/server";

  export let servers: ServerSelectOption[] = [];
  export let selected = "";

  function fts() {
    PrimaryState.navigate("fts");
  }

  function restart() {
    location.reload();
  }

  function apply() {
    setServer(selected);

    restart();
  }
</script>

{#if servers && servers.length}
  <div class="actions">
    <button on:click={fts}> Add Server </button>
    <button on:click={restart}> Restart </button>
    <button class="suggested" on:click={apply}> Continue </button>
  </div>
{/if}
