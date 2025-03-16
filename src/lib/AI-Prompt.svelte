<script>
  let { input } = $props();
</script>

<div>
  <textarea
    id="prompt"
    name="prompt"
    rows="4"
    cols="100"
    placeholder="What the hell do you want?"
    bind:value={input}
  ></textarea>
</div>

<style></style>
