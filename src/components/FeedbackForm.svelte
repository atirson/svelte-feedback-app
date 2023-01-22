<script>
  import Card from "./Card.svelte";
  import Button from "./Button.svelte";
  import RatingSelect from "./RatingSelect.svelte";

  let btnDisabled = true;
  let rating = 10;
  let minCaracterText = 10;
  let message;
  let text = '';

  const handleInput = () => {
    if (text.trim().length > minCaracterText) {
      btnDisabled = false;
      message = null;
    } else {
      btnDisabled = true;
      message = `Text must be at least ${minCaracterText} characters.`
    }
  };

  import { createEventDispatcher } from "svelte";

  const dispatch = createEventDispatcher();

  const handleSubmitForm = (e) => {
    const form = e.target;
    const formData = new FormData(form);
    const feedback = {
      id: Date.now(),
      rating: parseInt(formData.get("rating")),
      text,
    };
    dispatch("submit-feedback", feedback);
    form.reset();
  };
</script>

<Card>
  <header>
    <h2>How would you rate your service with us?</h2>
  </header>
  <form on:submit|preventDefault={handleSubmitForm}>
    <RatingSelect bind:value={rating} />
    <div class="input-group">
      <input type="text" on:input={handleInput} bind:value={text} placeholder="Tell us something that keeps you coming back" />
      <Button type="submit" disabled={btnDisabled}>Send</Button>
    </div>
    {#if message}
      <p class="message">{message}</p>
    {/if}
  </form>
</Card>

<style>
  header {
    max-width: 400px;
    margin: auto;
  }
  header h2 {
    font-size: 22px;
    font-weight: 600;
    text-align: center;
  }
  .input-group {
    display: flex;
    flex-direction: row;
    border: 1px solid #ccc;
    padding: 8px 10px;
    border-radius: 8px;
    margin-top: 15px;
  }
  input {
    flex-grow: 2;
    border: none;
    font-size: 16px;
  }
  input:focus {
    outline: none;
  }
  .message{
    padding-top: 10px;
    text-align: center;
    color: rebeccapurple;
  }
</style>
