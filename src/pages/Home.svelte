<script>
  import { onMount } from 'svelte';

  let visible = false;
  let count = 0;
  
  const dawits = [
    { text: 'DAWIT', style: 'font-size: 6rem; font-weight: 800;' },
    { text: 'dawit', style: 'font-size: 3rem; font-weight: 600;' },
    { text: 'dawit', style: 'font-size: 4rem; font-weight: 700; letter-spacing: 1rem;' },
    { text: 'DAWIT', style: 'font-size: 2rem; font-weight: 500; opacity: 0.7;' },
    { text: 'dawit', style: 'font-size: 5rem; font-weight: 800; font-style: italic;' },
    { text: 'dawit', style: 'font-size: 1.5rem; font-weight: 400; text-transform: uppercase;' },
    { text: 'DAWIT', style: 'font-size: 3.5rem; font-weight: 600; word-spacing: 2rem;' },
    { text: 'dawit', style: 'font-size: 2.5rem; font-weight: 500; letter-spacing: -2px;' },
    { text: 'dawit', style: 'font-size: 4.5rem; font-weight: 800; opacity: 0.5;' },
    { text: 'DAWIT', style: 'font-size: 1.8rem; font-weight: 400;' },
    { text: 'dawit', style: 'font-size: 3rem; font-weight: 700; text-decoration: underline;' },
    { text: 'DAWIT', style: 'font-size: 2.2rem; font-weight: 600;' },
  ];

  const links = [
    { href: '#/', label: 'Home' },
    { href: '#/about', label: 'About' },
    { href: '#/projects', label: 'Projects' },
    { href: '#/contact', label: 'Contact' },
    { href: 'https://www.youtube.com/watch?v=dQw4w9WgXcQ', label: '???' },
  ];

  onMount(() => {
    count = parseInt(localStorage.getItem('dawit-seen') || '0') + 1;
    localStorage.setItem('dawit-seen', count.toString());
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
    <h1 class="hero" class:visible>
      <span class="i-am">I am</span>
      <span class="dawit-main">DAWIT</span>
    </h1>
    
    <div class="dawit-grid">
      {#each dawits as dawit, i}
        <span 
          class="dawit-item" 
          class:visible
          style="animation-delay: {i * 0.08}s; {dawit.style}"
        >
          {dawit.text}
        </span>
      {/each}
    </div>

    <div class="marquee" class:visible>
      <div class="marquee-content">
        <span>dawit</span><span>dawit</span><span>dawit</span><span>dawit</span>
        <span>dawit</span><span>dawit</span><span>dawit</span><span>dawit</span>
        <span>dawit</span><span>dawit</span><span>dawit</span><span>dawit</span>
        <span>dawit</span><span>dawit</span><span>dawit</span><span>dawit</span>
      </div>
    </div>

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
    padding: 6rem 1rem 2rem;
    overflow: hidden;
  }

  .container {
    text-align: center;
    width: 100%;
  }

  .hero {
    font-size: clamp(3rem, 12vw, 8rem);
    font-weight: 800;
    margin: 0 0 2.5rem 0;
    display: flex;
    flex-direction: column;
    gap: 0.25rem;
    opacity: 0;
    transform: translateY(30px);
    transition: all 0.8s cubic-bezier(0.4, 0, 0.2, 1);
  }

  .hero.visible {
    opacity: 1;
    transform: translateY(0);
  }

  .i-am {
    font-size: 0.3em;
    font-weight: 400;
    color: hsl(220, 10%, 45%);
    letter-spacing: 0.4em;
    text-transform: uppercase;
  }

  .dawit-main {
    background: linear-gradient(135deg, hsl(280, 30%, 65%), hsl(200, 25%, 60%));
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
  }

  .dawit-grid {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    gap: 0.5rem 2rem;
    margin-bottom: 3rem;
    padding: 0 1rem;
  }

  .dawit-item {
    font-weight: 600;
    color: hsl(220, 10%, 55%);
    opacity: 0;
    transform: translateY(20px);
    transition: all 0.6s cubic-bezier(0.4, 0, 0.2, 1);
    white-space: nowrap;
  }

  .dawit-item.visible {
    opacity: 1;
    transform: translateY(0);
  }

  .dawit-item:hover {
    color: hsl(280, 25%, 65%) !important;
    transform: scale(1.1) translateY(0) !important;
  }

  .marquee {
    overflow: hidden;
    opacity: 0;
    transition: opacity 0.6s 0.8s;
    margin-bottom: 2rem;
  }

  .marquee.visible {
    opacity: 1;
  }

  .marquee-content {
    display: flex;
    animation: scroll 20s linear infinite;
    white-space: nowrap;
  }

  .marquee-content span {
    color: hsl(220, 10%, 20%);
    font-size: 1.5rem;
    font-weight: 700;
    padding: 0 1rem;
  }

  @keyframes scroll {
    0% { transform: translateX(0); }
    100% { transform: translateX(-50%); }
  }

  .count {
    color: hsl(220, 8%, 40%);
    font-size: 0.9rem;
    opacity: 0;
    transition: opacity 0.6s 1s;
  }

  .count.visible {
    opacity: 1;
  }
</style>
