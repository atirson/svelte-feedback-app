<script>
  import { createEventDispatcher } from "svelte";
  import Card from "./Card.svelte";

  export let item = {};

  const dispatch = createEventDispatcher();

  const handleDelete = (itemId) => {
    dispatch("delete-feedback", itemId);
  }
</script>

<Card>
    <div class="num-display">
      {item.rating}
    </div>
    <button on:click={() => handleDelete(item.id)} class="close">X</button>
    <p class="text-display">
      {item.text}
    </p>
</Card>

<style>
  .num-display {
    background: #ff6a95;
    color: #fff;
    border-radius: 50%;
    width: 50px;
    height: 50px;
    display: flex;
    justify-content: center;
    align-items: center;
    font-size: 1.5rem;
    position: absolute;
    top: -10px;
    left: -10px;
    padding: 10px;
    border: 2px solid #eee;
    text-align: center;
  }

  .close {
    position: absolute;
    top: 10px;
    right: 20px;
    cursor: pointer;

    background: none;
    border: none;
  }

  .text-display {
    margin-top: 0;
  }
</style>