<script>
  let { input } = $props();
</script>

<div>
  <textarea
    id="client-data"
    name="client-data"
    rows="4"
    cols="100"
    placeholder="What shitty data are we analyzing today?"
    bind:value={input}
  ></textarea>
</div>

<style></style>
