<script lang="ts">
  import { onMount } from "svelte";

  let hostname = ''

  onMount(() => {
    var elems = document.querySelectorAll('.dropdown-trigger');
    var instances = M.Dropdown.init(elems, {
      alignment: 'right'
    });

		hostname = window.location.hostname
  })
</script>

<svelte:head>
  <title>underwind.solutions</title> 
  <meta name="description" content="Websites are like sail boats. They require a main haul or backend API. They require a main mast or frontend interface. When put together and under the right wind-conditions/user-interations your boat/project can successfully navigate to it's destination." />
</svelte:head>

<div class="canvas hide-on-med-and-down">
  <div class="circles"></div>
</div>

<div class="wrapper">
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
              <a href="https://store.istrav.com" class="btn black">store</a>
              <a href="https://client-area.istrav.com" class="btn black">client area</a>
              <a href="https://entropy.underwind.solutions" class="btn black">entropy</a>
            </div>
          </div>
        </div>
      </div>
      <footer>
        <p style="margin: 0;">
          {hostname} © {new Date().getFullYear()}.
        </p>
        <p style="margin: 0;">
          With ❤️ by Travis Burandt
        </p>
      </footer>
      <br class="hide-on-med-and-down" />
      <br class="hide-on-med-and-down" />
      <br class="hide-on-med-and-down" />
      <br class="hide-on-med-and-down" />
      <br class="hide-on-med-and-down" />
      <br class="hide-on-med-and-down" />
    </div>
</div>

<style>
  :global(body) {
    position: inherit;
    width: 100%;
    height: 100%;
    margin: auto;
    overflow: auto;
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

  footer {
    color: #aaa;
    text-align: center;
  }

</style>