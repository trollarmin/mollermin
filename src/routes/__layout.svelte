<script context="module">
  /**
   * @type {import('@sveltejs/kit').Load}
   */
  export async function load({ page: { path } }) {
    return {
      props: {
        path
      }
    }
  }
</script>

<script lang="ts">
  import '../app.css'
  export let path = ''
  const links = [
    {
      href: '/',
      title: 'Home'
    },
    {
      href: '/logs',
      title: 'Logs'
    },
    {
      href: '/ranks',
      title: 'Ranks'
    }
  ]
</script>
<svelte:head>
  <link rel="icon" href="https://github.com/mollersuite.png" />
</svelte:head>
<header>
  <div
    class="icon"
    on:click={() => {
      new window.Audio('bark.mp3').play()
    }}
  />
  mollermin
  <nav>
    {#each links as link}
      <a href={link.href} class:selected={path === link.href}>{link.title}</a>
    {/each}
  </nav>
</header>
<main>
  <slot />
</main>

<style>
  @import url('https://rsms.me/inter/inter.css');
  main {
    flex: 1;
  }
  .icon {
    background-image: url(https://github.com/mollersuite.png),
      linear-gradient(to bottom, blue, black);
    width: 60px;
    height: 60px;
    display: inline-block;
    background-size: 30px, 100%;
    margin-right: 0.5em;
    background-repeat: no-repeat;
    background-position: center;
    border-radius: 50%;
    cursor: pointer;
    transition: background-size 1s;
  }

  .icon:hover {
    background-size: 25px, 100%;
  }

  .icon:active {
    background-size: 20px, 100%;
  }

  nav {
    margin-left: 0.5em;
    font-family: 'Inter', sans-serif;
  }
  nav a {
    margin-left: 0.5em;
    margin-right: 0.5em;
    text-decoration: overline;
    transition: text-decoration-thickness 0.5s;
    text-decoration-thickness: 0;
  }
  nav a:hover {
    text-decoration-thickness: 3px;
  }
  nav a.selected {
    text-decoration-thickness: 5px;
  }
  header {
    position: sticky;
    top: 0;
    border-bottom-right-radius: 50px;
    box-shadow: white 0 0 20px;
    overflow-x: auto;
    font-family: 'Inter Black', 'Inter Heavy', 'Inter', sans-serif;
    display: flex;
    justify-content: left;
    align-items: center;
    max-width: max-content;
    padding: 1em;
    user-select: none;
    background: rgb(61, 61, 61);
  }
</style>
