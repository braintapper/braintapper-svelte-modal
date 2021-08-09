<script>

  import { createEventDispatcher } from 'svelte';
  import { Button }  from "braintapper-svelte-button";
  import ModalContainer from "./Container.svelte"

  let dispatch = createEventDispatcher();

  export let entity = "item";
  export let show = false;

  let destroy = function () {
    dispatch("destroy");
  }
  let cancel = function () {
    dispatch("cancel");
  }
</script>


<ModalContainer {show} on:cancel={cancel}>
  <div slot="header">
    Delete this {entity}?
  </div>
  <div slot="footer">
    <div>
      <Button on:click={destroy} state="critical">Delete</Button>
      <Button on:click={cancel} state="cancel">Cancel</Button>
    </div>
  </div>
  <div>
    Are you sure you want to do this?
  </div>
</ModalContainer>

