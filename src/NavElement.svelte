<script>
  export let active;
  export let book;

  import { createEventDispatcher } from "svelte";
  const dispatch = createEventDispatcher();

  function onClickNav() {
    dispatch("navClicked", { book });
  }
</script>

<style type="text/scss">
  .nav-tab-list-el {
    min-width: 100px;
    margin: 16px 16px 0;
    opacity: 0.5;
    &.active {
      opacity: 1;
    }
    .book-thumb {
      height: 100px;
    }
  }
</style>

<li class="nav-tab-list-el" class:active on:click={onClickNav}>
  <img class="book-thumb" src={book.imgUrl} />
</li>
