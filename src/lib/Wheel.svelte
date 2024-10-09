<script lang="ts">
  import { anxietyWheel } from "../constants/wheels";

  let items = anxietyWheel;

  const itemDegrees = 360 / items.length;
  const spokeDegrees = 180 / items.length;

  let wheelNode: HTMLButtonElement | null = null;

  const toggleSpinning = () => {
    if (wheelNode) {
      wheelNode.classList.add("spinning");
      setTimeout(() => {
        if (wheelNode) {
          wheelNode.style.transform = "rotate(180deg)";
          wheelNode.classList.remove("spinning");
        }
      }, 1000);
    }
  };
</script>

<button
  class="wheel-container"
  bind:this={wheelNode}
  on:click={() => toggleSpinning()}
>
  {#each items as wheelItem, idx}
    <div class="wheel-item" style="transform: rotate({itemDegrees * idx}deg);">
      <div
        class="wheel-text"
        style={itemDegrees * idx > 90 && itemDegrees * idx < 270
          ? "transform: rotate(180deg); justify-content: end;"
          : ""}
      >
        {wheelItem}
      </div>
    </div>
    <div
      class="spoke"
      style="transform: rotate({itemDegrees * idx + spokeDegrees}deg)"
    />
  {/each}
</button>

<style>
  .wheel-container {
    width: 400px;
    height: 400px;
    margin: auto;
    outline: 4px solid black;
    background-color: purple;
    border-radius: 99999px;
    display: block;
    border: none;
    position: relative;
  }
  .wheel-item {
    position: absolute;
    /* top: calc(200px - 12px); */
    width: calc(200px - 12px);
    color: white;
    transform-origin: 100% 50%;
    /* padding-left: 12px; */
  }
  .spoke {
    position: absolute;
    /* top: 198px; */
    background-color: white;
    width: calc(200px - 12px);
    color: white;
    transform-origin: 100% 50%;
    height: 4px;
  }
  .wheel-text {
    display: flex;
  }
  :global(.wheel-container.spinning) {
    animation: spinning 4s ease-in forwards;
  }
  @keyframes spinning {
    0% {
      transform: rotate(0deg);
    }
    100% {
      transform: rotate(180deg);
    }
  }
</style>
