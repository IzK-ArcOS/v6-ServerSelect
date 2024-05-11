<script lang="ts">
  import { ConnectIcon } from "$ts/images/general";
  import { getAllServers, removeServer } from "$ts/server/multi";
  import { PrimaryState } from "$ts/states";
  import { ServerSelectOption } from "$types/server";

  export let server: ServerSelectOption;
  export let selected: string;
  export let update: () => any;

  function select() {
    selected = server.hostname;
  }

  function remove() {
    removeServer(server.hostname);

    const servers = getAllServers();

    if (!servers.length) return PrimaryState.navigate("fts");

    selected = servers[0];

    update();
  }
</script>

<button class="option" on:click={select} class:selected={selected == server.hostname}>
  <img src={ConnectIcon} alt="" class="icon" />
  <p class="caption">{server.hostname}</p>
  <div class="right">
    {#if server.private}
      <span class="material-icons-round">lock</span>
    {/if}
    <button class="delete material-icons-round" on:click={remove}>delete</button>
  </div>
</button>
