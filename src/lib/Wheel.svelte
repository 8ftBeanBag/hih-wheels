<script>
  import { anxietyWheel } from "../constants/wheels";

  let items = anxietyWheel;

  const itemDegrees = 360 / items.length;
  const spokeDegrees = 180 / items.length;
  console.log(items.length, 360 / items.length);
</script>

<div class="wheel-container">
  <div class="wheel-items-parent">
    {#each items as wheelItem, idx}
      <div
        class="wheel-item"
        style="transform: rotate({itemDegrees * idx}deg);"
      >
        {wheelItem}
      </div>
      <div
        class="spoke"
        style="transform: rotate({itemDegrees * idx + spokeDegrees}deg)"
      />
    {/each}
  </div>
</div>

<style>
  .wheel-container {
    width: 400px;
    height: 400px;
    margin: auto;
    outline: 4px solid black;
    background-color: purple;
    border-radius: 99999px;
  }
  .wheel-items-parent {
    position: relative;
  }
  .wheel-item {
    position: absolute;
    top: calc(200px - 12px);
    width: calc(200px - 12px);
    color: white;
    transform-origin: 100% 50%;
    padding-left: 12px;
    border: 1px solid black;
  }
  .spoke {
    position: absolute;
    top: 198px;
    background-color: white;
    width: 200px;
    color: white;
    transform-origin: 100% 50%;
    height: 4px;
  }
</style>
