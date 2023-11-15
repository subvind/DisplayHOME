<script lang="ts">
  import { onMount } from "svelte";

  import { AuthAccountRegister } from "subvind-components"

	let organization: any;

  onMount(async () => {
    let homeHostname = window.location.hostname
    if (homeHostname === 'localhost') {
      homeHostname = 'www.subvind.com'
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

<br />
<br />
<AuthAccountRegister organization={organization} />

<style>
  :global(body) {
    background: #eee !important;
  }
</style>