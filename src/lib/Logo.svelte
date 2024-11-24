<script lang="ts">
  import { onMount } from 'svelte';
  import { wait } from 'utils/wait';

  interface Props {
    onAnimationComplete(): void;
  }

  let { onAnimationComplete: animationCompleteCallback }: Props = $props();

  let cursorIndex = $state(0);
  let animationComplete = $state(false);

  const letters = [
    ...'thorsson'.split('').map((letter) => ({ letter, suffix: false })),
    ...'.dev'.split('').map((letter) => ({ letter, suffix: true })),
    { letter: ' ', suffix: false },
  ];

  onMount(async () => {
    await wait(1900);

    for (let i = 0; i < letters.length; i++) {
      const curr = letters.at(i)?.letter || '';
      const next = letters.at(i + 1)?.letter || '';
      const delay = curr > next ? 200 : next < curr ? 150 : 100;

      cursorIndex = i;

      await wait(delay);
    }

    await wait(2000);

    animationComplete = true;

    animationCompleteCallback();
  });
</script>

<h1>
  {#each letters as { letter, suffix }, index}
    <span
      class:suffix
      class:hidden={index >= cursorIndex}
      class:cursor={index === cursorIndex}
      class:cursor-blink={index === cursorIndex && !animationComplete}
      class:cursor-fade-out={index === cursorIndex && animationComplete}
    >
      {letter}
    </span>
  {/each}
</h1>

<style>
  h1 {
    display: flex;
    letter-spacing: -4%;
    font-weight: 600;
  }

  h1 span {
    position: relative;
    display: inline-block;
    white-space: pre;
  }

  .suffix {
    font-weight: 400;
    color: var(--color-fg-secondary);
  }

  .hidden {
    color: transparent;
  }

  .cursor::after {
    position: absolute;
    pointer-events: none;
    content: ' ';
    width: '100%';
    height: '100%';
    top: 0;
    left: 0;
    background-color: var(--color-fg-primary);
  }

  .cursor-blink::after {
    animation: blink 1000ms 250ms infinite;
  }

  @keyframes blink {
    0% {
      opacity: 1;
    }
    30% {
      opacity: 0;
    }
    60% {
      opacity: 0;
    }
    100% {
      opacity: 1;
    }
  }

  .cursor-fade-out::after {
    animation: fadeOut 1000ms forwards;
  }

  @keyframes fadeOut {
    0% {
      opacity: 1;
    }
    100% {
      opacity: 0;
    }
  }
</style>
