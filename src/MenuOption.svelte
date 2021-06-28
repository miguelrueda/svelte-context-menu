<script>
  import { onMount, getContext } from "svelte";
  import { key } from "./menu.js";

  export let isDisabled = false;
  export let text = "";

  import { createEventDispatcher } from "svelte";
  const dispatch = createEventDispatcher();

  const { dispatchClick } = getContext(key);

  const handleClick = (e) => {
    if (isDisabled) return;

    dispatch("click");
    dispatchClick();
  };
</script>

<div class:disabled={isDisabled} on:click={handleClick} class="dropdown">
  <!-- {#if text}
    {text}
  {:else}
    <slot />
  {/if} -->
  <span>
    <slot />
  </span>
  <div class="dropdown-content">
    <slot name="dropdown-content" />
  </div>
</div>

<style lang="scss">
  div.dropdown {
    padding: 4px 15px;
    cursor: default;
    font-size: 14px;
    display: flex;
    align-items: center;
    grid-gap: 5px;
  }
  div.dropdown:hover {
    background: #0002;
  }
  div.disabled {
    color: #0006;
  }
  div.disabled:hover {
    background: white;
  }

  .dropdown:hover > .dropdown-content {
    display: block;
  }
  .dropdown-content {
    padding: 4px 15px;
    cursor: default;
    font-size: 14px;
    display: flex;
    align-items: center;
    grid-gap: 5px;

    position: absolute;
    top: 0;
    right: -150px;
    width: 150px;
    list-style: none;
    padding: 0;
    margin: 0;
    display: none;
  }
</style>
