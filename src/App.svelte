<script lang="ts">
  import { onMount } from 'svelte';
  import Link from 'lib/Link.svelte';
  import Logo from 'lib/Logo.svelte';

  let showContent = $state(false);
  let contentHeight = $state(0);
  let section: HTMLElement;

  const revealAnimationDuration = 1300;

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
    <h2 class:stagger-reveal={showContent} style="--stagger-delay: 500ms">
      Freelance software developer based in Gothenburg, Sweden.
    </h2>
    <nav>
      <div class:stagger-reveal={showContent} style="--stagger-delay: 600ms">
        <Link to="https://github.com/pthorsson">Github</Link>
      </div>
      <div class:stagger-reveal={showContent} style="--stagger-delay: 700ms">
        <Link to="https://linkedin.com/in/pthorsson">LinkedIn</Link>
      </div>
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
