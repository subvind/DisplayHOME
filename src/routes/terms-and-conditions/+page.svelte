<script lang="ts">
	import { onMount } from "svelte";

	let organization: any;

	onMount(async () => {
		let homeHostname = window.location.hostname
		if (homeHostname === 'localhost') {
			homeHostname = 'demo.subvind.com'
		}

    const responseOrg = await fetch(`https://api.subvind.com/organizations/homeHostname/${homeHostname}`, {
      method: 'GET',
      headers: {
        'Content-Type': 'application/json',
      }
    });

    if (responseOrg.ok) {
      organization = await responseOrg.json();
    } else {
      const errorData = await responseOrg.json();
      alert(errorData.error);
    }
		
		// @ts-ignore
		gtag('event', 'pageview', {
			'organizationId': organization.id
		});
	})
</script>

<svelte:head>
	{#if organization}
		<title>Terms & Conditions - {organization.displayName}</title>
	{/if}
	<meta name="description" content="About this app" />
</svelte:head>

<nav class="breadcrumbs black">
  <div class="container">
    <div class="nav-wrapper">
      <div class="col s12">
        <a href="/" class="breadcrumb">Home</a>
				<a href="/terms-and-conditions" class="breadcrumb">Terms & Conditions</a>
      </div>
    </div>
  </div>
</nav>

<br />
<br />

<div class="container">
	<h4>Terms & Conditions</h4>

	{#if organization}
		{@html organization.termsAndConditions}
	{:else}
		<p>loading...</p>
	{/if}
</div>

<br />
<br />

<style>
	nav {
		position: relative;
	}

	.container {
		color: #fff;
	}
</style>