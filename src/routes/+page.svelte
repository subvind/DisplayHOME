<script lang="ts">
  import { onMount } from "svelte";

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

    var elems = document.querySelectorAll('.dropdown-trigger2');
    var instances = M.Dropdown.init(elems, {
      alignment: 'right'
    });

		// @ts-ignore
		gtag('event', 'pageview', {
			'organizationId': organization.id
		});
  })
</script>

<svelte:head>
  <title>underwind.solutions</title> 
  <meta name="description" content="Websites are like sail boats. They require a main haul or backend API. They require a main mast or frontend interface. When put together and under the right wind-conditions/user-interations your boat/project can successfully navigate to it's destination." />
</svelte:head>

<div class="container">
  <br class="hide-on-med-and-down" />
  <br class="hide-on-med-and-down" />
  <br />
  <div class="row">
    <div class="col s12 m1">
    </div>
    <div class="col s12 m10">
      <div style="text-align: center;">
        <a href="/">
          <img src="./anchor.png" alt="underwind.solutions" class="logo">
        </a>
      </div>
      <div class="card" style="width: 100%;">
        <div class="card-image">
          <img src="sailboat.jpg">
          <span class="card-title">underwind.solutions</span>
        </div>
        <a class="dropdown-trigger2 btn-floating btn-large waves-effect waves-light black right" style="margin: -2em 2em 0 0;" href='#' data-target='dropdown0'><i class="material-icons">share</i></a>

        <!-- Dropdown Structure -->
        <ul id='dropdown0' class='dropdown-content' style="width: 200px;">
          <li><a href="https://www.youtube.com/channel/UCwcibF78LrLQBpfvlApvgKg" target="_blank">YouTube</a></li>
          <li><a href="https://twitter.com/BurandtTravis" target="_blank">Twitter</a></li>
          <li><a href="https://github.com/subvind" target="_blank">GitHub</a></li>
        </ul>
        <div class="card-content">
          {#if organization}
            {@html organization.about}
          {/if}
        </div>
        {#if organization && organization.menu}
          <div class="card-action">
            {#each organization.menu as menu}
              <a href={menu.url} class="btn black menu">{menu.name}</a>
            {/each}
          </div>
        {/if}
      </div>
    </div>
  </div>
</div>

<style>
  .logo {
    position: relative;
    width: 10em;
    margin-bottom: -5.5em;
    z-index: 1;
  }

  .menu {
    margin: 0.5em 1em 0.5em 0;
  }
</style>