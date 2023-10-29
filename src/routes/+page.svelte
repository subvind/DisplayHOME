<script lang="ts">
  import { onMount } from "svelte";

  onMount(() => {
    var elems = document.querySelectorAll('.dropdown-trigger');
    var instances = M.Dropdown.init(elems, {
      alignment: 'right'
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
        <a class="dropdown-trigger btn-floating btn-large waves-effect waves-light black right" style="margin: -2em 2em 0 0;" href='#' data-target='dropdown1'><i class="material-icons">share</i></a>

        <!-- Dropdown Structure -->
        <ul id='dropdown1' class='dropdown-content' style="width: 200px;">
          <li><a href="https://www.youtube.com/channel/UCwcibF78LrLQBpfvlApvgKg" target="_blank">YouTube</a></li>
          <li><a href="https://twitter.com/BurandtTravis" target="_blank">Twitter</a></li>
          <li><a href="https://github.com/subvind" target="_blank">GitHub</a></li>
        </ul>

        <div class="card-content">
          Hello There!
          <br />
          Thank you for taking the time in reviewing us for your consideration.
          <br />
          <br />
          Websites are like sail boats. They require a main haul or backend API. They require a main mast or frontend interface. When put together and under the right wind-conditions/user-interations your boat/project can successfully navigate to it's destination.
          <br />
          <blockquote cite="">
            <a href="https://underwind.solutions">https://underwind.solutions</a>
          </blockquote>
          Say hello to underwind.solutions: where your project is not just another website; because we treat your project as if it were a high end yacht. We're not as expensive as you might think though, as we only charge per request. So no wind-under-you-sails/user-interactions then no movement/charge.
          <br />
          <br />
          Therefore, the better user experience we create, the more user-interactions your website will get, thus the more profit we can both make. 
          <br />
          <br />
          A wind wind situation :)
          <br />
          <br />
          kind regards,
          <br />
          underwind // subvind
        </div>
        <div class="card-action">
          <a href="https://subvind.com" class="btn black">portfolio</a>
          <a href="https://istrav.com" class="btn black">website</a>
          <a href="https://videos.istrav.com" class="btn black">videos</a>
          <a href="https://store.istrav.com" class="btn black">store</a>
          <a href="https://client-area.istrav.com" class="btn black">client area</a>
          <a href="https://entropy.underwind.solutions" class="btn black">entropy</a>
        </div>
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
</style>