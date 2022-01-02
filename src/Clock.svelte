<script>
	export let time;
     import {sharedData} from "./shared.js";
     sharedData.subscribe(value => {
          time = new Date(value);
          console.log(value);
     });
</script>

<main>
	<div id="time">
          {time}
     </div>
</main>

<style>
	
</style>