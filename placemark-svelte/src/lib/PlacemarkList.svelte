<script>
  import { onMount } from "svelte";
  import { placemarkService } from "../services/placemark-service";

  let placemarkList = [];
  onMount(async () => {
      placemarkList = await placemarkService.getPlacemarks();
  });
</script>

<table class="table is-fullwidth">

  <tbody>
      {#each placemarkList as placemark}
      <div class="box box-link-hover-shadow">
        <h2 class="title">
                  {placemark.title}
                  <a href="/place" class="button is-rounded">
                    <span style="color: grey;">
                    <i class="fas fa-folder-open"></i>
                    </span>
                  </a>
                  </h2>
                  </div>
      {/each}
  </tbody>
</table>
