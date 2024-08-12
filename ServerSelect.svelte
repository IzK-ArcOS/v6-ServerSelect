<script lang="ts">
  import { ConnectIcon } from "$ts/images/general";
  import { getAllServers, getServer } from "$ts/server/multi";
  import { PrimaryState } from "$ts/states";
  import { sleep } from "$ts/util";
  import { ServerSelectOption } from "$types/server";
  import { onMount } from "svelte";
  import Selector from "./Components/Selector.svelte";
  import "./css/main.css";

  let selected = "";
  let servers: ServerSelectOption[] = [];
  let show = false;

  onMount(async () => {
    if (!getAllServers().length) {
      PrimaryState.navigate("fts");
      return;
    }

    selected = getServer();

    await sleep(500);

    show = true;
  });
</script>

<div class="serverselect theme-system fullscreen" class:show>
  <div class="content">
    <div class="header">
      <div class="text">
        <h1>Where do you want to go today?</h1>
        <p class="sub">Choose the server you want to connect to, then click Continue.</p>
      </div>
      <div class="right">
        <img src={ConnectIcon} alt="" />
      </div>
    </div>
    <Selector bind:selected bind:servers />
  </div>
</div>
