<script lang="ts">
  let _message: string | undefined;
  let _timeout: number | undefined;

  export function notify(message: string) {
    clearTimeout(_timeout);
    _message = message;
    _timeout = setTimeout(() => {
      _message = undefined;
    }, 5000);
  }
</script>

{#if _message}
  <div class="notification">
    <div class="background">
      <h1>{_message}</h1>
    </div>
  </div>
{/if}

<style>
  .notification {
    width: 100%;
    height: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
    font-size: 5vw;
    text-shadow: 3px 4px 7px rgba(81, 67, 21, 0.8);
  }

  .background {
    padding: 32px;
    background-color: #000000ee;
    border-radius: 8px;
  }
</style>
