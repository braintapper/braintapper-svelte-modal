<script>

  import ModalHeader from "./Header.svelte";
  import ModalBody from "./Body.svelte";
  import ModalFooter from "./Footer.svelte";

  import { createEventDispatcher } from 'svelte';
  
  let dispatch = createEventDispatcher();
  
  
  export let show = false;
  
  let modal = undefined;

  let handleKeydown = function (e) {
    if (e.key == 'Escape') {
      dispatch("cancel");
    }
  }

  let setVisibility = function (state) {
    if (state) {
      document.body.style = "overflow:hidden";
    } else {
      document.body.style = "";
    }
  }


  $: setVisibility(show);

</script>



<svelte:window on:keydown={handleKeydown}/>
{#if show}
  <modal-background></modal-background>
  <modal role="dialog" aria-modal="true" bind:this={modal}>
      <ModalHeader>
          <slot name="header"/>
      </ModalHeader>
      <ModalBody>
          <slot/>
      </ModalBody>
      <ModalFooter>
          <slot name="footer"/>
      </ModalFooter>
  </modal>
{/if}


<style>

  modal-background {
    position: fixed;
    display: block;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: rgba(0, 0, 0, 0.3);
    z-index: 1000;
  }

  modal {
    display: block;
    position: fixed;
    left: 50%;
    top: 50%;
    width: calc(100vw - 4em);
    max-width: 32em;
    max-height: calc(100vh - 4em);
    overflow: show;
    transform: translate(-50%, -50%);
    padding: 24px;
    border-radius: 8px;
    background: white;
    z-index: 1001;
  }

</style>
