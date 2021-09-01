<script context="module">
  import { browser, dev } from '$app/env'

  // we don't need any JS on this page, though we'll load
  // it in dev so that we get hot module replacement...
  export const hydrate = true //dev

  // ...but if the client-side router is already loaded
  // (i.e. we came here from elsewhere in the app), use it
  export const router = browser

  // since there's no dynamic data here, we can prerender
  // it so that it gets served as a static asset in prod
  export const prerender = false //true
</script>

<script>
  import { supabase, user } from '$lib/supabase'
</script>

<svelte:head>
  <title>Home</title>
</svelte:head>
<article>
  {#if $user}
    <h1>Welcome, {$user.role}!</h1>
    <button on:click={supabase.auth.signOut.bind(supabase.auth)}>Log out</button
    >
  {:else}
    <h1>are you a bragle?</h1>
    <input
      on:click={() =>
        supabase.auth.signIn({
          provider: 'discord'
        })}
      type="image"
      name="Name of image button"
      src="/smell.jpg"
      alt="Molly smelling an unauthorized user"
    />
    <p>please login to confirm you are indeed a bragle</p>
  {/if}
</article>

<style>
  article {
    text-align: center;
  }
  h1 {
    font-family: monospace;
  }
  input {
    cursor: default;
    color: white;
    background: none;
    max-width: 500px;
    min-width: 0;
    width: 100vw;
  }
</style>
