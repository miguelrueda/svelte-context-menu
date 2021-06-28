<script>
  import Menu from "./Menu.svelte";
  import MenuOption from "./MenuOption.svelte";
  import MenuDivider from "./MenuDivider.svelte";
  import { tick } from "svelte";

  import Icon from "./Icon.svelte";

  let pos = { x: 0, y: 0 };
  let showMenu = false;

  async function onRightClick(e) {
    if (showMenu) {
      showMenu = false;
      await new Promise((res) => setTimeout(res, 100));
    }

    pos = { x: e.clientX, y: e.clientY };
    showMenu = true;
  }

  function closeMenu() {
    showMenu = false;
  }
</script>

{#if showMenu}
  <Menu {...pos} on:click={closeMenu} on:clickoutside={closeMenu}>
    <MenuOption on:click={console.log}>
      <div class="text-item">Dropdown 1 ></div>
      <div slot="dropdown-content">
        <MenuOption on:click={console.log}>
          <span>Dropwdown1</span>
        </MenuOption>
        <MenuOption on:click={console.log}>
          <span>Dropwdown1</span>
        </MenuOption>
      </div>
    </MenuOption>
    <MenuOption on:click={console.log}>
      <span>Do nothing, but twice</span>
    </MenuOption>
    <MenuDivider />
    <MenuOption isDisabled={true} on:click={console.log}>
      <span>Whoops, disabled!</span>
    </MenuOption>
    <MenuOption on:click={console.log}>
      <div>
        <Icon />
        <span>Look! An icon!</span>
      </div>
    </MenuOption>
  </Menu>
{/if}

<svelte:body on:contextmenu|preventDefault={onRightClick} />

<style lang="scss">
  .dropdown {
    &:hover > .dropdown-content {
      display: block;
    }
  }
  .dropdown-content {
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
