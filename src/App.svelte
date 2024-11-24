<script lang="ts">
  import { onMount } from 'svelte';
  import Link from './lib/Link.svelte';
  import Logo from './lib/Logo.svelte';

  let showContent = $state(false);
  let contentHeight = $state(0);
  let section: HTMLElement;

  const revealAnimationDuration = 1500;

  onMount(() => {
    contentHeight = section.scrollHeight;
  });
</script>

<main style="--reveal-animation-duration: {revealAnimationDuration}ms">
  <Logo
    onAnimationComplete={() => {
      showContent = true;
    }}
  />
  <section
    bind:this={section}
    class:show={showContent}
    style="--content-height: {contentHeight}px"
  >
    <h2>Freelance software developer based in Gothenburg, Sweden.</h2>
    <nav>
      <Link to="https://github.com/pthorsson">Github</Link>
      <Link to="https://linkedin.com/in/pthorsson">LinkedIn</Link>
    </nav>
  </section>
</main>

<style>
  section {
    display: flex;
    flex-direction: column;
    padding-top: 0;
    gap: 2rem;
    opacity: 0;
    transition: all var(--reveal-animation-duration);
    height: 0px;
  }

  section.show {
    opacity: 1;
    padding-top: 1.75rem;
    height: var(--content-height);
  }

  nav {
    display: flex;
    flex-direction: column;
    gap: 0.5rem;
  }
</style>
