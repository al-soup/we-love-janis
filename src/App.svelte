<script lang="ts">
  // TODO replace favicon
  type Compliment = {
    text: string;
    maxLength: number;
  };
  // TODO add more colors like lightblue
  let color: string = "#f4d03f";

  // TODO get maxLength from data
</script>

<main style="--color: {color};">
  <div class="words">
    <span>J</span>
    <span>A</span>
    <span>N</span>
    <span>I</span>
    <span>S</span>
  </div>

  <div class="words">
    <span>H</span>
    <span>Ö</span>
    <span>R</span>
    <span>T</span>
  </div>

  <div class="words">
    <span>G</span>
    <span>U</span>
    <span>T</span>
    <span>&nbsp;</span>
    <span>Z</span>
    <span>U</span>
  </div>
  <div class="words">
    <span>G</span>
    <span>U</span>
    <span>T</span>
    <span>&nbsp;</span>
    <span>Z</span>
    <span>U</span>
  </div>
</main>

<style lang="scss">
  main {
    font-family: "Archivo Black", sans-serif;
    background: var(--color);
    display: flex;
    flex-direction: column;
    height: 100vh;
    height: 100svh;
    justify-content: center;
    align-items: center;
  }

  .words {
    color: var(--color);
    font-size: 0;
    line-height: 1.5;
  }

  .words span {
    font-size: 5rem;
    display: inline-block;
    animation: move 3s ease-in-out infinite;
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

  .words span {
    @for $i from 2 through 11 {
      &:nth-child(#{$i}) {
        animation-delay: 0.5s + ($i - 2) * 0.5s;
      }
    }
  }
</style>
