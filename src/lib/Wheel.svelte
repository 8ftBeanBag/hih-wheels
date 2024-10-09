<script lang="ts">
  import { anxietyWheel } from "../constants/wheels";

  let items = anxietyWheel;

  const itemDegrees = 360 / items.length;
  const spokeDegrees = 180 / items.length;

  let wheelNode: HTMLButtonElement | null = null;
  const min = 360;
  const limit = 3600;
  let spinDegrees = min;

  const toggleSpinning = () => {
    let max = Math.floor(Math.random() * limit);
    spinDegrees = Math.random() * (max - min) + min;
    console.log(spinDegrees);
    if (wheelNode) {
      wheelNode.style.transform = `rotate(${spinDegrees}deg)`;
    }
  };
</script>

<button
  class="wheel-container"
  bind:this={wheelNode}
  on:click={() => toggleSpinning()}
>
  {#each items as wheelItem, idx}
    <div
      class="wheel-item"
      style="transform: rotate(
      {itemDegrees * idx}deg); --spin-degrees: {spinDegrees}deg;"
    >
      {wheelItem}
    </div>
    <div
      class="spoke"
      style="transform: rotate({itemDegrees * idx + spokeDegrees}deg)"
    />
  {/each}
</button>

<style>
  .wheel-container {
    width: calc(2 * var(--wheel-width));
    height: calc(2 * var(--wheel-width));
    margin: auto;
    outline: var(--wheel-border-w) solid black;
    background-color: purple;
    border-radius: 99999px;
    display: block;
    padding: 0;
    border: none;
    transition: transform 2s;
  }
  .wheel-item {
    position: absolute;
    width: var(--wheel-width);
    color: white;
    transform-origin: 100% 50%;
  }
  .spoke {
    position: absolute;
    background-color: white;
    width: var(--wheel-width);
    color: white;
    transform-origin: 100% 50%;
    height: 1px;
  }
</style>
