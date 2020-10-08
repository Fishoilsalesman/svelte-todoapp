<script>
  export let showModal = false;
</script>

<style>
  .backdrop {
    width: 100%;
    height: 100%;
    position: fixed;
    background: rgba(0, 0, 0, 0.6);
  }
  .modal {
    padding: 50px 10px;
    border-radius: 10px;
    max-width: 400px;
    margin: 10% auto;
    text-align: center;
    background: white;
  }
</style>

{#if showModal}
  <div class="backdrop" on:click|self>
    <div class="modal">
      <slot />
    </div>
  </div>
{/if}
