
<div >
  <button on:click={getInfo}>Get Stats</button>

  <p>{posts.name} </p>
  <p>{posts.race}</p>
  <p>{posts.class}</p>
</div>
<label>
<input type="checkbox" bind:checked={visible} >
visible
</label>
<div class="container">   
    {#if visible}
   
		<canvas transition:fade id="myChart" width="100" height="50"></canvas>
{/if}
 
  </div>
<div class="container">
    <button on:click={createDungeonChart}>Dugeon Stats</button>
      <canvas id="myNewChart" width="100" height="50"></canvas>
  </div>
  <div class="container">
    <button on:click={createLineChart}>Dugeon Stats Line</button>
      <canvas id="myLineChart" width="100" height="50"></canvas>
  </div>

<script>
import { onMount } from 'svelte';
import { fade } from 'svelte/transition';
let visible = true;

function createLineChart() {
    //options
  var options = {
    responsive: true,
    title: {
      display: true,
      position: "top",
      text: "Line Graph",
      fontSize: 18,
      fontColor: "#111"
    },
    legend: {
      display: true,
      position: "bottom",
      labels: {
        fontColor: "#333",
        fontSize: 16
      }
    }
  };
var ctx = document.getElementById('myLineChart');
var myLineChart = new Chart(ctx, {
    type: 'line',
    data:{
    labels: ["match1", "match2", "match3", "match4", "match5"],
    datasets: [
      {
        label: "TeamA Score",
        data: [10, 50, 25, 70, 40],
        borderColor: 'rgba(192, 192, 192, 1)',
        backgroundColor: 'rgba(192, 192, 192, 0.2)',
        fill: true,
        lineTension: .3,
        radius: 5
      },
      {
        label: "TeamB Score",
        data: [20, 35, 40, 60, 50],
        borderColor: 'rgba(75, 192, 192, 1)',
        backgroundColor: 'rgba(75, 192, 192, 0.2)',
        fill: true,
        lineTension: .3,
        radius: 5
      }
    ]
    },
    options:options
  });
}
  

  

  function createChart() {

var ctx = document.getElementById('myChart');
var myChart = new Chart(ctx, {
    type: 'bar',
    data: {
        labels: ['Normal', 'Heroic', 'Mythic'],
        datasets: [{
            label: 'Ny’alotha Completion Chart',
            data: [12, 9, 1],
            backgroundColor: [
                'rgba(255, 99, 132, 0.33)',
                'rgba(54, 162, 235, 0.33)',
                'rgba(255, 206, 86, 0.33)',
                
            ],
            borderColor: [
                'rgba(255, 99, 132, 1)',
                'rgba(54, 162, 235, 1)',
                'rgba(255, 206, 86, 1)',
              
            ],
            borderWidth: 2
        }]
    },
    options: {
        scales: {
            yAxes: [{
                ticks: {
                    beginAtZero: true
                }
            }]
        }
    }
});
  }
  function createDungeonChart() {


var ctx2 = document.getElementById('myNewChart');
var myChart = new Chart(ctx2, {
    type: 'bar',
    data: {
        labels: ['Dungeon x', 'Dungeon y', 'Dungeon z'],
        datasets: [{
            label: 'Ny’alotha Completion Chart For ',
            data: [22.52, 29.75, 35.16],
            backgroundColor: [
                'rgba(255, 99, 132, 0.33)',
                'rgba(54, 162, 235, 0.33)',
                'rgba(255, 206, 86, 0.33)',
                
            ],
            borderColor: [
                'rgba(255, 99, 132, 1)',
                'rgba(54, 162, 235, 1)',
                'rgba(255, 206, 86, 1)',
              
            ],
            borderWidth: 2
        }]
    },
    options: {
        scales: {
            yAxes: [{
                ticks: {
                    beginAtZero: true
                }
            }]
        }
    }
});
  }
 let name='jmd';
  let posts = [];
  let getInfo = (async () =>{
       const res= await fetch("https://raider.io/api/v1/characters/profile?region=us&realm=area52&name=jmd&fields=mythic_plus_best_runs%3Aall");
       posts = await res.json();
 });
 onMount(createChart);

</script>



 