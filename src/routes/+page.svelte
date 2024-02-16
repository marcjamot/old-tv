<script lang="ts">
  import Notification from "$lib/Notification.svelte";
  import Video from "$lib/Video.svelte";
  import Volume from "$lib/Volume.svelte";
  import { onMount } from "svelte";

  const VIDEOS = [
    {
      name: "Hemliga Svensson",
      url: "/movies/hemliga-svensson-1933.webm",
    },
    {
      name: "Hemsöborna",
      url: "/movies/hemsoborna.webm",
    },
  ] as const;

  let i = 0;
  let notification: Notification;
  let video: Video;
  let volume = 10;

  onMount(async () => {
    video.play(VIDEOS[i].url);
    document.body.requestPointerLock();
  });

  function onKeydown(e: KeyboardEvent) {
    switch (e.key) {
      case "ArrowLeft":
        channelDown();
        break;
      case "ArrowRight":
        channelUp();
        break;
      case "ArrowDown":
        volumeDown();
        break;
      case "ArrowUp":
        volumeUp();
        break;
    }
  }

  function channelDown() {
    i -= 1;
    if (i < 0) {
      i = VIDEOS.length - 1;
    }
    notification.notify(VIDEOS[i].name);
    video.play(VIDEOS[i].url);
  }

  function channelUp() {
    i += 1;
    if (i >= VIDEOS.length) {
      i = 0;
    }
    notification.notify(VIDEOS[i].name);
    video.play(VIDEOS[i].url);
  }

  function volumeDown() {
    volume -= 1;
    if (volume < 0) {
      volume = 0;
    }
    notification.notify(`Volym ${volume}`);
    video.volume(volume);
  }

  function volumeUp() {
    volume += 1;
    if (volume > 10) {
      volume = 10;
    }
    notification.notify(`Volym ${volume}`);
    video.volume(volume);
  }
</script>

<main>
  <div class="video">
    <Video bind:this={video} />
  </div>
  <!-- <div class="volume">
    <Volume bind:volume />
  </div> -->
  <div class="notification">
    <Notification bind:this={notification} />
  </div>
</main>

<svelte:window on:keydown={onKeydown} />

<style>
  main {
    position: relative;
    width: 100%;
    height: 100%;
  }

  .video {
    width: 100%;
    height: 100%;
  }

  .notification {
    position: absolute;
    left: 0;
    right: 0;
    top: 0;
    bottom: 0;
  }
</style>
