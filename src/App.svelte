<script>
  import Router from 'svelte-spa-router';
  import Home from './pages/Home.svelte';
  import About from './pages/About.svelte';
  import Projects from './pages/Projects.svelte';
  import Contact from './pages/Contact.svelte';

  const routes = {
    '/': Home,
    '/about': About,
    '/projects': Projects,
    '/contact': Contact,
  };
</script>

<Router {routes} />
