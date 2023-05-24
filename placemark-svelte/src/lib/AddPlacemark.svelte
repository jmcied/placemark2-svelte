<script>
    import { onMount } from "svelte";
  import { goto } from '$app/navigation';
  import { placemarkService } from "../services/placemark-service";

  let placemarkList = [];
  let title = '';
  let message = "Please add a new Placemark";

  onMount(async () => {
    placemarkList = await placemarkService.getPlacemarks();
    });

  async function addPlacemark() {
    if (title) {
      const placemark = {
        title: title
      };
      const success = await placemarkService.addPlacemarks(placemark);
          if (!success) {
                message = "placemark not added - some error occurred";
                return;
            }
            message = "Thanks! Your placemark has been added";
            goto("/placemark");
        } else {
            message = "Please complete all requested fields";
        }
      } 
</script>

<form on:submit|preventDefault={addPlacemark}>
  <div class="field">
      <label class="label" for="placemark">Title</label>
      <input bind:value={title} class="input" id="title" name="title" placeholder="Enter Placemark" type="text" />
  </div>

  <div class="field is-grouped">
      <button class="button is-link">Add Placemark</button>
  </div>
  <div class="box">
    {message}
</div>
</form>