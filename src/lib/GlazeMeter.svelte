<script>
  let { value } = $props();
</script>

<div class="slidecontainer">
  <label for="myRange">AI Glaze Meter</label>
  <input
    type="range"
    min="1"
    max="100"
    bind:value
    class="slider"
    id="myRange"
  />
</div>

<style>
  #myRange {
    width: 100%;
  }
</style>
