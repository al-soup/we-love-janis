<script lang="ts">
  import { colors, textCollection } from "./data";
  // TODO replace favicon
  let color: string;
  let texts: string[];

  async function infiniteLoop() {
    texts = textCollection[getRandomIndex(textCollection)];
    color = colors[getRandomIndex(colors)];

    const longest = texts.reduce((a, b) => (a.length > b.length ? a : b));

    await sleep(1000 * (longest.length + 2));

    infiniteLoop();
  }

  function sleep(ms: number) {
    return new Promise((resolve) => setTimeout(resolve, ms));
  }

  function getRandomIndex(array: any[]): number {
    return Math.floor(Math.random() * array.length);
  }

  infiniteLoop();
</script>

<main style="--color: {color};">
  {#key JSON.stringify(texts)}
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
    font-family: "Archivo Black", sans-serif;
    background-color: var(--color);
    display: flex;
    flex-direction: column;
    height: 100vh;
    height: 100svh;
    justify-content: center;
    align-items: center;
    transition: background-color 1s ease, color 1s ease;
    color: var(--color);
  }

  .text {
    font-size: 0;
    line-height: 1.5;
  }

  .text span {
    font-size: 5rem;
    display: inline-block;
    animation: move 3s ease-in-out 2;
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

  @media (max-width: 380px) {
    .text span {
      font-size: 3.5;
    }
  }
</style>
