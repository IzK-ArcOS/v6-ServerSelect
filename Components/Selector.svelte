<script lang="ts">
  import { getAuthcode } from "$ts/server/authcode";
  import { getAllServers } from "$ts/server/multi";
  import { ServerSelectOption } from "$types/server";
  import { onMount } from "svelte";
  import Actions from "./Actions.svelte";
  import Option from "./Selector/Option.svelte";

  export let selected = "";
  export let servers: ServerSelectOption[] = [];

  async function update() {
    servers = [];

    const list = getAllServers().sort();

    for (let i = 0; i < list.length; i++) {
      const ac = getAuthcode(list[i]);

      servers.push({
        hostname: list[i],
        private: !!ac,
        authCode: ac,
      });
    }
  }

  onMount(update);
</script>

<div class="selector">
  <div class="options">
    {#each servers as server}
      <Option {server} bind:selected {update} />
    {/each}
  </div>
  <Actions {selected} {servers} />
</div>
