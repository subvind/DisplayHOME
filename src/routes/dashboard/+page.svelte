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
		<title>Dashboard - {organization.displayName}</title>
	{/if}
	<meta name="description" content="A wind wind situation :)" />
</svelte:head>

<iframe src="https://dashboard.underwind.solutions/public-dashboards/23f9f9e2ea934bddb53e69e2f1ed6864" sandbox="allow-same-origin allow-scripts" frameborder="0"></iframe>

<br />
<br />

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