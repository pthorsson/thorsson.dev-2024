<script lang="ts">
  import type { Snippet } from 'svelte';

  interface Props {
    to: string;
    children: Snippet;
  }

  let { to, children }: Props = $props();
</script>

<a href={to} target="_blank">
  {@render children()}
  <svg fill="none" viewBox="0 0 35 15" class="arrow">
    <path d="M1 6.375h19v2.25H1z" />
    <g class="arrow-head">
      <path d="M16 6.375h16v2.25H16z" />
      <path
        fill-rule="evenodd"
        clip-rule="evenodd"
        d="M31.79 7.5 25.5 1h3l5.095 5.306a1.75 1.75 0 0 1 0 2.388L28.5 14h-3l6.29-6.5Z"
      />
    </g>
  </svg>
</a>

<style>
  a {
    align-self: self-start;
    font-weight: 600;
    color: currentColor;
    text-decoration: none;
    font-size: 1.25rem;
    padding: 0.25em;
    margin-left: -0.25em;
  }

  .arrow {
    height: 1rem;
    margin-bottom: -0.05em;
  }

  .arrow * {
    fill: currentColor;
    transition: all 150ms;
  }

  .arrow-head {
    transform: translateX(-0.25em);
  }

  a:hover .arrow-head {
    transform: translateX(0em);
  }

  a:hover .arrow {
    color: var(--color-fg-secondary);
  }
</style>
