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

  const shapes = [
    'dawit',
    'dawit',
    'dawit',
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
  <div class="container">
    <div class="circle c1" class:visible>
      <span>DAWIT</span>
    </div>
    <div class="circle c2" class:visible>
      <span>dawit</span>
    </div>
    <div class="circle c3" class:visible>
      <span>DAWIT</span>
    </div>
    
    <h1 class:dawit={visible}>DAWIT</h1>
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

  .container {
    text-align: center;
    position: relative;
  }

  .circle {
    position: absolute;
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    opacity: 0;
    transform: scale(0);
    transition: all 1s cubic-bezier(0.4, 0, 0.2, 1);
  }

  .circle.visible {
    opacity: 1;
    transform: scale(1);
  }

  .circle span {
    font-weight: 700;
    color: hsl(220, 10%, 60%);
  }

  .c1 {
    width: 300px;
    height: 300px;
    border: 2px solid hsl(280, 20%, 30%);
    top: -100px;
    left: -150px;
    animation: rotate 30s linear infinite;
  }

  .c2 {
    width: 200px;
    height: 200px;
    border: 2px solid hsl(200, 20%, 25%);
    bottom: -50px;
    right: -100px;
    animation: rotate 25s linear infinite reverse;
  }

  .c3 {
    width: 150px;
    height: 150px;
    border: 2px solid hsl(160, 15%, 25%);
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%) scale(0);
  }

  .c3.visible {
    transform: translate(-50%, -50%) scale(1);
    animation: pulse 3s ease-in-out infinite;
  }

  @keyframes rotate {
    to { transform: rotate(360deg); }
  }

  @keyframes pulse {
    0%, 100% { transform: translate(-50%, -50%) scale(1); }
    50% { transform: translate(-50%, -50%) scale(1.1); }
  }

  h1 {
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
    transition-delay: 0.3s;
  }

  h1.dawit {
    opacity: 1;
    transform: scale(1);
  }

  .count {
    color: hsl(220, 8%, 40%);
    font-size: 0.9rem;
    margin-top: 2rem;
    opacity: 0;
    transition: opacity 0.6s 0.8s;
  }

  .count.visible {
    opacity: 1;
  }
</style>
