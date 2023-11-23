<script lang="ts">
  import { onMount } from "svelte";

  import { HeaderDefault } from "subvind-components"
  import Footer from "$lib/Footer.svelte"

  let organization: any;
	let homeHostname: any = '';

  onMount(async () => {
    homeHostname = window.location.hostname
    if (homeHostname === 'localhost') {
      homeHostname = 'istrav.homenomy.subvind.com'
    }
    const response = await fetch(`https://api.subvind.com/organizations/homeHostname/${homeHostname}`, {
      method: 'GET',
      headers: {
        'Content-Type': 'application/json',
      }
    });

    if (response.ok) {
      organization = await response.json();
    } else {
      const errorData = await response.json();
      alert(errorData.error);
    }
  })
</script>

<div class="canvas hide-on-med-and-down">
  <div class="circles"></div>
</div>

<div class="wrapper">
  {#if organization}
    <HeaderDefault organization={organization} />
  {:else}
    <nav class="grey darken-3">
      <div class="nav-wrapper">
      </div>
    </nav>
  {/if}

  <slot />

  <Footer organization={organization} />
</div>

<style>
  :global(body) {
    position: inherit;
    width: 100%;
    height: 100%;
    margin: auto;
    overflow-x: hidden;
    background: linear-gradient(
      -90deg,
      #000 0%,
      #222 100%
    );
  }

  .wrapper {
    /* position: relative;
    height: 100%;
    overflow: auto; */
  }

  .logo {
    position: relative;
    width: 10em;
    margin-bottom: -5.5em;
    z-index: 1;
  }

  .canvas::before,
  .canvas::after,
  .canvas > .circles,
  .canvas > .circles::before,
  .canvas > .circles::after {
    filter: blur(200px);
  }

  .canvas::before,
  .canvas::after {
    position: absolute;
    content: "";
    width: 750px;
    height: 750px;
    border-radius: 100%;
  }

  .canvas::before {
    background: #00806d;
    top: -500px;
    left: -300px;
  }

  .canvas::after {
    background: #ff0000;
    right: -600px;
    top: 50%;
    transform: translateY(-50%);
  }

  .canvas > .circles,
  .canvas > .circles::before,
  .canvas > .circles::after {
    border-radius: 100%;
    position: absolute;
  }

  .canvas > .circles::before,
  .canvas > .circles::after {
    content: "";
    width: 140px;
    height: 140px;
    top: 50%;
    transform: translateY(-50%);
  }

  .canvas > .circles {
    width: 500px;
    height: 500px;
    background: #41A5F5;
    bottom: -300px;
    left: -200px;
  }

  .canvas > .circles::before {
    background: #41A5F5;
    left: -40%;
  }

  .canvas > .circles::after {
    background: #41A5F5;
    right: -20%;
  }

</style>