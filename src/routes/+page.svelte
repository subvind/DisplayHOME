<script lang="ts">
  import { onMount } from "svelte";

  import 'bytemd/dist/index.css'
  import { Editor, Viewer } from 'bytemd'
  import gfm from '@bytemd/plugin-gfm'

  const plugins = [
    gfm(),
    // Add more plugins here
  ]

  let organization: any;
	let homeHostname: any = '';
  let description: string;
  let about: string;

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

    // remove html from text
    var html = organization.description;
    var html2 = organization.about;
    var div = document.createElement("div");
    var div2 = document.createElement("div");
    div.innerHTML = html;
    div2.innerHTML = html2;
    description = div.textContent || div.innerText || "";
    about = div2.textContent || div2.innerText || "";
  })
</script>

<svelte:head>
  {#if organization}
    <title>{organization.displayName} - {description}</title> 
  {/if}
  <meta name="description" content={about} />
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
          {#if organization}
            {#if organization.orgPhoto}
              <img src={`https://s3.us-east-2.amazonaws.com/${organization.orgname}.${organization.orgPhoto.bucket.name}/${organization.orgPhoto.filename}`} alt="logo" class="logo">
            {:else}
              <img src="/anchor.png" alt="logo" class="logo">
            {/if}
          {/if}
        </a>
      </div>
      <div class="card z-depth-5" style="width: 100%;">
        <div class="card-image">
          {#if organization}
            {#if organization.splashPhoto}
              <img src={`https://s3.us-east-2.amazonaws.com/${organization.orgname}.${organization.splashPhoto.bucket.name}/${organization.splashPhoto.filename}`} alt="splash">
            {:else}
              <div class="banner"></div>
            {/if}
          {/if}
          <span class="card-title">{window.location.hostname}</span>
        </div>
        <a class="dropdown-trigger2 btn-floating btn-large waves-effect waves-light black right" style="margin: -2em 2em 0 0;" href='#' data-target='dropdown0'><i class="material-icons">share</i></a>

        <!-- Dropdown Structure -->
        <ul id='dropdown0' class='dropdown-content' style="width: 200px;">
          {#if organization}
            {#if organization.ebayUser}
              <li><a href={`https://www.ebay.com/usr/${organization.ebayUser}`} target="_blank">eBay</a></li>
            {/if}
            {#if organization.etsyShop}
              <li><a href={`https://www.etsy.com/shop/${organization.etsyShop}`} target="_blank">etsy</a></li>
            {/if}
            {#if organization.youtubeChannel}
              <li><a href={`https://www.youtube.com/${organization.youtubeChannel}`} target="_blank">YouTube</a></li>
            {/if}
            {#if organization.twitterUser}
              <li><a href={`https://twitter.com/${organization.twitterUser}`} target="_blank">Twitter</a></li>
            {/if}
            {#if organization.githubUser}
              <li><a href={`https://github.com/${organization.githubUser}`} target="_blank">GitHub</a></li>
            {/if}
          {/if}
        </ul>
        <div class="card-content">
          {#if organization}
            <Viewer value={organization.about} {plugins} />
          {/if}
        </div>
        {#if organization && organization.menu && organization.menu.length}
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
  
  .banner {
    height: 300px;
    background-color: #e5e5f7;
    opacity: 1;
    background-image: linear-gradient(30deg,#9b9b9b 12%,transparent 12.5%,transparent 87%,#9b9b9b 87.5%,#9b9b9b),linear-gradient(150deg,#9b9b9b 12%,transparent 12.5%,transparent 87%,#9b9b9b 87.5%,#9b9b9b),linear-gradient(30deg,#9b9b9b 12%,transparent 12.5%,transparent 87%,#9b9b9b 87.5%,#9b9b9b),linear-gradient(150deg,#9b9b9b 12%,transparent 12.5%,transparent 87%,#9b9b9b 87.5%,#9b9b9b),linear-gradient(60deg,#9b9b9b77 25%,transparent 25.5%,transparent 75%,#9b9b9b77 75%,#9b9b9b77),linear-gradient(60deg,#9b9b9b77 25%,transparent 25.5%,transparent 75%,#9b9b9b77 75%,#9b9b9b77);
    background-size: 80px 140px;
    background-position: 0 0,0 0,40px 70px,40px 70px,0 0,40px 70px;
  }

  .card-title {
    text-shadow: -2px 1px black
  }
</style>