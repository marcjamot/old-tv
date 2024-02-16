<script lang="ts">
  export let volume: number;
</script>

<div class="volume">
  {#each [...Array(10).keys()] as i}
    <div class="bar" class:active={i + 1 <= volume} />
  {/each}
</div>

<style>
  .volume {
    display: flex;
    flex-direction: column-reverse;
    justify-content: space-between;
  }

  .bar {
    width: 64px;
    height: 16px;
    background-color: transparent;
    border: 0px solid green;
  }

  .active {
    background-color: green;
  }
</style>
