
<script lang="ts">
  export let organization: any;
</script>

<footer>
  <p style="margin: 0;">
    {window.location.hostname} © {new Date().getFullYear()}.
  </p>
  {#if organization && organization.isBranding}
    <p style="margin: 0;">
      powered by <a href="https://subvind.com">subvind.com</a>
    </p>
  {/if}
</footer>
<br class="hide-on-med-and-down" />
<br class="hide-on-med-and-down" />
<br class="hide-on-med-and-down" />
<br class="hide-on-med-and-down" />
<br class="hide-on-med-and-down" />
<br class="hide-on-med-and-down" />

<style>
  footer {
    color: #aaa;
    text-align: center;
  }

  :global(.no-splash footer) {
    color: #111;
  }
</style>