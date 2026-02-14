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

  const bigDawit = [
    { text: 'DAWIT', size: 'clamp(4rem, 15vw, 12rem)', weight: 900, opacity: 0.15 },
    { text: 'dawit', size: 'clamp(3rem, 10vw, 8rem)', weight: 800, opacity: 0.1 },
    { text: 'DAWIT', size: 'clamp(2rem, 8vw, 6rem)', weight: 700, opacity: 0.08 },
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
  <div class="bg">
    {#each bigDawit as d, i}
      <span 
        class="bg-dawit" 
        style="
          font-size: {d.size}; 
          font-weight: {d.weight}; 
          opacity: {d.opacity};
          animation-delay: {i * 0.2}s;
        "
        class:visible
      >
        {d.text}
      </span>
    {/each}
  </div>

  <div class="content">
    <h1 class:dawit={visible}>
      <span class="d">D</span><span class="a">a</span><span class="w">w</span><span class="i">i</span><span class="t">t</span>
    </h1>
    <p class="count" class:visible>Seen {count} times</p>
  </div>
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
    align-items: center;
    justify-content: center;
    padding: 6rem 2rem 2rem;
    position: relative;
    overflow: hidden;
  }

  .bg {
    position: absolute;
    inset: 0;
    display: flex;
    align-items: center;
    justify-content: center;
    pointer-events: none;
  }

  .bg-dawit {
    position: absolute;
    font-weight: 900;
    color: hsl(280, 20%, 50%);
    white-space: nowrap;
    opacity: 0;
    transform: scale(0.8);
    transition: all 1.5s cubic-bezier(0.4, 0, 0.2, 1);
  }

  .bg-dawit.visible {
    opacity: inherit;
    transform: scale(1);
  }

  .content {
    position: relative;
    z-index: 1;
    text-align: center;
  }

  h1 {
    font-size: clamp(4rem, 20vw, 15rem);
    font-weight: 800;
    margin: 0;
    line-height: 1;
    display: flex;
  }

  h1.dawit .d { 
    animation: letter 0.5s cubic-bezier(0.4, 0, 0.2, 1) forwards;
    opacity: 0;
    transform: translateY(50px);
    transition-delay: 0s;
  }
  h1.dawit .a { 
    animation: letter 0.5s cubic-bezier(0.4, 0, 0.2, 1) forwards;
    opacity: 0;
    transform: translateY(50px);
    transition-delay: 0.1s;
  }
  h1.dawit .w { 
    animation: letter 0.5s cubic-bezier(0.4, 0, 0.2, 1) forwards;
    opacity: 0;
    transform: translateY(50px);
    transition-delay: 0.2s;
  }
  h1.dawit .i { 
    animation: letter 0.5s cubic-bezier(0.4, 0, 0.2, 1) forwards;
    opacity: 0;
    transform: translateY(50px);
    transition-delay: 0.3s;
  }
  h1.dawit .t { 
    animation: letter 0.5s cubic-bezier(0.4, 0, 0.2, 1) forwards;
    opacity: 0;
    transform: translateY(50px);
    transition-delay: 0.4s;
  }

  @keyframes letter {
    to {
      opacity: 1;
      transform: translateY(0);
    }
  }

  h1.dawit span {
    background: linear-gradient(135deg, hsl(280, 30%, 65%), hsl(200, 25%, 60%));
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
  }

  .count {
    color: hsl(220, 8%, 40%);
    font-size: 0.9rem;
    margin-top: 2rem;
    opacity: 0;
    transition: opacity 0.6s 0.6s;
  }

  .count.visible {
    opacity: 1;
  }
</style>
