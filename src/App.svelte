<script lang="ts">
  import { colors, textCollection } from "./data";

  let color: string;
  let texts: string[];
  let renderKey: number;

  async function loopInfinite() {
    texts = textCollection[getRandomIndex(textCollection)];
    color = colors[getRandomIndex(colors)];

    const longest = texts.reduce((a, b) => (a.length > b.length ? a : b));

    await sleep(1000 * (longest.length + 2));
    // trigger a re-render of the animation
    renderKey = new Date().getTime();

    loopInfinite();
  }

  function sleep(ms: number) {
    return new Promise((resolve) => setTimeout(resolve, ms));
  }

  function getRandomIndex(array: any[]): number {
    return Math.floor(Math.random() * array.length);
  }

  loopInfinite();
</script>

<main style="--color: {color};">
  {#key renderKey}
    {#each texts as text}
      <div class="text">
        {#each text as character}
          <span>{@html character.replace(" ", "&nbsp;")}</span>
        {/each}
      </div>
    {/each}
  {/key}
</main>

<style lang="scss">
  main {
    align-items: center;
    background-color: var(--color);
    color: var(--color);
    display: flex;
    flex-direction: column;
    font-family: "Archivo Black", sans-serif;
    height: 100svh;
    height: 100vh;
    justify-content: center;
    transition: background-color 1.5s ease, color 1.5s ease;
  }

  .text {
    font-size: 0;
    line-height: 1.5;
  }

  .text span {
    animation: move 3s ease-in-out 2;
    display: inline-block;
    font-size: 5rem;
  }

  @keyframes move {
    0% {
      transform: translate(-30%, 0);
    }
    50% {
      text-shadow: 0 25px 50px rgba(0, 0, 0, 0.75);
    }
    100% {
      transform: translate(30%, 0);
    }
  }

  .text span {
    @for $i from 2 through 14 {
      &:nth-child(#{$i}) {
        animation-delay: 0.5s + ($i - 2) * 0.5s;
      }
    }
  }

  @media (max-width: 400px) {
    .text span {
      font-size: 3rem;
    }
  }
</style>
