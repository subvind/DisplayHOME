<script lang="ts">
	import { onMount, onDestroy } from "svelte";

	let organization: any;
	let childOrganizations: any;
  
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

    /**
     * fetch child orgs
     */
		const responseChildOrg = await fetch(`https://api.subvind.com/organizations/childRelated/${organization.id}`, {
      method: 'GET',
      headers: {
        'Content-Type': 'application/json',
      }
    });

    if (responseChildOrg.ok) {
      childOrganizations = await responseChildOrg.json();
      console.log('childOrganizations', childOrganizations)
    } else {
      const errorData = await responseChildOrg.json();
      alert(errorData.error);
    }
	})
</script>

<svelte:head>
	{#if organization}
		<title>Organizations - {organization.displayName}</title>
	{/if}
	<meta name="description" content="About this app" />
</svelte:head>

<nav class="breadcrumbs black">
  <div class="container">
    <div class="nav-wrapper">
      <div class="col s12">
        <a href="/" class="breadcrumb">Home</a>
				<a href="/organizations" class="breadcrumb">Organizations</a>
      </div>
    </div>
  </div>
</nav>

<div class="container">
	{#if organization}
		<h4>Current:</h4>
		<div class="row">
			<div class="col s12 m6 l6">
				<div class="card hoverable">
					<div class="card-image">
						<div class="photo">
							{#if organization.splashPhoto}
								<img src={`https://s3.us-east-2.amazonaws.com/${organization.orgname}.${organization.splashPhoto.bucket.name}/${organization.splashPhoto.filename}`} alt="organization">
							{:else}
								<img src="/placeholder2.png" alt="organization">
							{/if}
						</div>
						<!-- <span class="card-title black-text">NFS</span> -->
					</div>
					<div class="card-content">
						{#if organization.orgPhoto}
							<img src={`https://s3.us-east-2.amazonaws.com/${organization.orgname}.${organization.orgPhoto.bucket.name}/${organization.orgPhoto.filename}`} alt="logo" class="logo">
						{:else}
							<img src="/anchor.png" alt="logo" class="logo">
						{/if}
						<h5 style="margin: 0;">{organization.displayName}</h5>
						<p>{@html organization.description}</p>
					</div>
					<div class="card-action">
						<a href={`https://${organization.homeHostname}/organizations`} target="_blank">{organization.homeHostname}</a>
					</div>
				</div>
			</div>
		</div>
	{/if}
	{#if childOrganizations}
		<h4>Affiliates:</h4>
		{#if childOrganizations.subOrganizations.length}
			<div class="row organizations">
				<div class="col s12 cards-container">
					{#each childOrganizations.subOrganizations as org}
						<div class="card hoverable">
							<div class="card-image">
								<div class="photo">
									{#if org.splashPhoto}
										<img src={`https://s3.us-east-2.amazonaws.com/${org.orgname}.${org.splashPhoto.bucket.name}/${org.splashPhoto.filename}`} alt="organization">
									{:else}
										<img src="/placeholder2.png" alt="organization">
									{/if}
								</div>
								<!-- <span class="card-title black-text">NFS</span> -->
							</div>
							<div class="card-content">
								{#if org.orgPhoto}
									<img src={`https://s3.us-east-2.amazonaws.com/${org.orgname}.${org.orgPhoto.bucket.name}/${org.orgPhoto.filename}`} alt="logo" class="logo">
								{:else}
									<img src="/anchor.png" alt="logo" class="logo">
								{/if}
								<h5 style="margin: 0;">{org.displayName}</h5>
								<p>{@html org.description}</p>
							</div>
							<div class="card-action">
								<a href={`https://${org.homeHostname}/organizations`} target="_blank">{org.homeHostname}</a>
							</div>
						</div>
					{/each}
				</div>
			</div>
		{:else}
			<p>There are none.</p>
		{/if}
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

  .organizations {
    width: 100%;
  }

	.logo {
		float: left;
		width: 50px;
		margin-right: 1em;
	}

  .cards-container {
    column-break-inside: avoid;
  }
  .cards-container .card {
    display: inline-block;
    overflow: visible;
  }

  @media only screen and (max-width : 600px) {
    .cards-container {
      -webkit-column-count: 1;
      -moz-column-count: 1;
      column-count: 1;
    }
  }
  @media only screen and (min-width : 601px) {
    .cards-container {
      -webkit-column-count: 1;
      -moz-column-count: 1;
      column-count: 1;
    }
  }
  @media only screen and (min-width : 993px) {
    .cards-container {
      -webkit-column-count: 2;
      -moz-column-count: 2;
      column-count: 2;
    }
  }
</style>