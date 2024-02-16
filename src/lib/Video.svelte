<script lang="ts">
  let video: HTMLVideoElement;
  let _volume = 1;

  export async function play(src: string) {
    video.src = src;
    await video.play();
    video.volume = _volume;
    video.currentTime = 0;
  }

  export function volume(value: number) {
    _volume = value / 10;
    video.volume = _volume;
  }
</script>

<video bind:this={video}>
  <track kind="captions" />
</video>

<style>
  video {
    width: 100%;
    height: 100%;
  }
</style>
