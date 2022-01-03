<script>
	import {sharedData} from "./shared.js";

     function updateTime() {
          var form = document.forms[0];
          if (form.time.value &&
              form.date.value &&
              form.timezone.value) {
               
               if ( form.plusminustz.value == "-" &&
                    ((form.timezone.value > 12) ||
                    (form.timezone.value == 12 && form.minuteoffsettz.value == 30))
                  ) {
                    return alert("Timezones can be from -12:00 to +14:00.");
               } 
               
               var newTime = [form.time.value, form.date.value, form.plusminustz.value + form.timezone.value + ":" + form.minuteoffsettz.value];
               var newTimeString = newTime[1] + "T" + newTime[0] + ":00.000" + newTime[2];
               sharedData.update(s => newTimeString);
          } else {
               return alert("Please fill out all the fields correctly.");
          }
     }
</script>

<main>
	<form on:submit|preventDefault={updateTime}>
          <label for="time">Time:</label>
          <input name="time" type="time"><br>

          <label for="date">Date:</label>
          <input name="date" type="date"><br>

          <label for="plusminustz">Timezone:</label>
          <select name="plusminustz">
               <option value="+">+</option>
               <option value="-">-</option>
          </select>
          <input name="timezone" type="number" min="0" max="14" onchange="if(parseInt(this.value,10)<10)this.value='0'+this.value;">:
          <select name="minuteoffsettz">
               <option value="00">00</option>
               <option value="30">30</option>
          </select><br>
          <input type="submit" value="Get all timezones ->">
     </form>
</main>

<style>
	
</style>