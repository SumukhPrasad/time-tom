<script>
	export let time;
     var timeString = "";
     import {sharedData} from "./shared.js";
     import {aryIannaTimeZones} from "./timezones.js";
     sharedData.subscribe(value => {
          time = new Date(value);
          timeString = value;
     });
     function filter(input) {
          // Declare variables 
          var input, filter, table, tr, td, i, txtValue;
          filter = input.toUpperCase();
          table = document.getElementById("timeTable");
          tr = table.getElementsByTagName("tr");

          // Loop through all table rows, and hide those who don't match the search query
          for (i = 0; i < tr.length; i++) {
               td = tr[i].getElementsByTagName("td")[0];
               if (td) {
                    txtValue = td.textContent || td.innerText;
                    if (txtValue.toUpperCase().indexOf(filter) > -1) {
                         tr[i].style.display = "";
                    } else {
                         tr[i].style.display = "none";
                    }
               } 
          }              
     }

</script>

<main>
	<div id="time">
          <b>Given time String</b>: <i>{timeString}</i><br>
          <b>GMT time</b>: <i>{time.toGMTString()}</i><br>
          <b>Local time</b>: <i>{time.toString()}</i><br>
     </div>
     <input on:keyup={({ target: { value } }) => filter(value)} type="text" id="filterInput" placeholder="Filter timezones..."><br>
     <table id="timeTable">
          <tr>
               <th>Timezone (City)</th>
               <th>Timezone (Full)</th>
               <th>Time/date in timezone</th>
          </tr>
          {#each aryIannaTimeZones as tz}
               <tr>
                    <td>{tz[1]}</td>
                    <td>{tz[0]}</td>
                    <td>{
                         time.toLocaleString("en-US", {
                              timeZone: `${tz[0]}`
                         })
                         }</td>
               </tr>
	     {/each}
     </table>
</main>

<style>
	tr:hover {
          background-color: #006cff;
          color: white;
     }
</style>