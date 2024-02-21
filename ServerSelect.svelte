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

<div class="serverselect theme-dark fullscreen" class:show>
  <window class="ss-inner visible glass bigtb focused">
    <div class="titlebar">
      <div class="title">
        <span class="title-wrapper">
          <img src={ConnectIcon} alt="" />
          <span class="title-text">Choose Server</span>
        </span>
      </div>
    </div>
    <div class="body">
      <!-- <div class="left">
        <img src={ConnectIcon} alt="" class="logo" />
      </div> -->
      <Selector bind:selected bind:servers />
    </div>
  </window>
</div>
