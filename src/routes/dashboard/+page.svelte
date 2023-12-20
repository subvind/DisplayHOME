<script lang="ts">
	import { onMount, onDestroy } from "svelte";

	let organization: any;

	onDestroy(() => {
    document.body.classList.remove('no-splash');
  });

	onMount(async () => {
		document.body.classList.add('no-splash');
		
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
		<title>Privacy Policy - {organization.displayName}</title>
	{/if}
	<meta name="description" content="About this app" />
</svelte:head>

<iframe src="https://dashboard.underwind.solutions/public-dashboards/d9c9ca81b1c64ea4ad09c8e13f621cdb" sandbox="allow-same-origin allow-scripts" frameborder="0"></iframe>

<style>
	iframe {
		position: absolute;
		right: 0;
		bottom: 0;
		left: 0;
		width: 100%;
		height: calc(100vh - 64px);
	}
</style>