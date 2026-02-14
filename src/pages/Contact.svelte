<script>
  import { onMount } from 'svelte';

  let visible = false;
  let count = 0;

  const links = [
    { href: '#/', label: 'Home' },
    { href: '#/about', label: 'About' },
    { href: '#/projects', label: 'Projects' },
    { href: '#/contact', label: 'Contact' },
    { href: 'https://www.youtube.com/watch?v=dQw4w9WgXcQ', label: '???' },
  ];

  const rows = [
    'dawit dawit dawit dawit dawit',
    'dawit dawit dawit dawit dawit',
    'dawit dawit dawit dawit dawit',
    'dawit dawit dawit dawit dawit',
    'dawit dawit dawit dawit dawit',
  ];

  onMount(() => {
    count = parseInt(localStorage.getItem('dawit-seen') || '0');
    setTimeout(() => visible = true, 100);
  });
</script>

<nav>
  {#each links as link}
    <a href={link.href}>{link.label}</a>
  {/each}
</nav>

<main>
  <div class="grid" class:visible>
    {#each rows as row, i}
      <div class="row" style="animation-delay: {i * 0.1}s">
        {#each row.split(' ') as word, j}
          <span class="dawit" style="animation-delay: {j * 0.05 + i * 0.1}s">{word}</span>
        {/each}
      </div>
    {/each}
  </div>

  <h1 class:dawit={visible}>DAWIT</h1>
  <p class="count" class:visible>Seen {count} times</p>
</main>

<style>
  nav {
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    display: flex;
    justify-content: center;
    gap: 2rem;
    padding: 1rem;
    background: hsl(220, 8%, 8%);
    border-bottom: 1px solid hsl(220, 10%, 15%);
    z-index: 100;
  }

  a {
    color: hsl(220, 8%, 50%);
    text-decoration: none;
    font-size: 0.9rem;
    transition: color 0.2s;
  }

  a:hover, a:global(.active) {
    color: hsl(280, 25%, 65%);
  }

  main {
    min-height: 100vh;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    padding: 6rem 2rem 2rem;
    position: relative;
    overflow: hidden;
  }

  .grid {
    position: absolute;
    inset: 0;
    display: flex;
    flex-direction: column;
    justify-content: center;
    gap: 0.25rem;
    opacity: 0;
    transition: opacity 0.6s;
  }

  .grid.visible {
    opacity: 1;
  }

  .row {
    display: flex;
    justify-content: center;
    gap: 0.5rem;
    overflow: hidden;
  }

  .dawit {
    font-size: 1rem;
    font-weight: 600;
    color: hsl(220, 10%, 18%);
    animation: fall 2s ease-in forwards;
    opacity: 0;
  }

  @keyframes fall {
    0% {
      opacity: 0;
      transform: translateY(-20px);
    }
    50% {
      opacity: 1;
    }
    100% {
      opacity: 0;
      transform: translateY(20px);
    }
  }

  .grid.visible .dawit {
    animation: none;
    opacity: 1;
    transition: all 0.3s;
  }

  .grid.visible .dawit:hover {
    color: hsl(280, 25%, 65%);
    transform: scale(1.2);
  }

  h1 {
    position: relative;
    z-index: 1;
    font-size: clamp(4rem, 20vw, 15rem);
    font-weight: 800;
    margin: 0;
    background: linear-gradient(135deg, hsl(280, 30%, 65%), hsl(200, 25%, 60%));
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
    opacity: 0;
    transform: scale(0.8);
    transition: all 1s cubic-bezier(0.4, 0, 0.2, 1);
  }

  h1.dawit {
    opacity: 1;
    transform: scale(1);
  }

  .count {
    position: relative;
    z-index: 1;
    color: hsl(220, 8%, 40%);
    font-size: 0.9rem;
    margin-top: 2rem;
    opacity: 0;
    transition: opacity 0.6s 0.5s;
  }

  .count.visible {
    opacity: 1;
  }
</style>
