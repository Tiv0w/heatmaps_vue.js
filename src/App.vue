<template>
    <div id="app">
        <vue-plot :data="data" :layout="layout" />
        <button @click="generateDataset">Appuyez ici pour de nouvelles donn&eacutees</button>
    </div>
</template>

<script>
 /* use plotly.js through vue-plotly
  * quickly create a heatmap of the visitor numbers,
  * taking in axes days of the week and hour of the day
  */
 import VuePlotly from '@statnett/vue-plotly'
 
 
 export default {
     name: 'app',

     components: {
         'vue-plot': VuePlotly 
     },
     
     data() {
         return {
             data: [{
                 z: null,
                 x: ['Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday', 'Sunday'],
                 y: null,
                 type: 'heatmap',
                 colorscale: 'Cividis'
             }],
             
             layout: {
                 title: 'Affluence sur une semaine',
                 width: 800,
                 height: 800,
                 autosize: false
             }
         }
     },
     
     mounted() {
         this.createChart();
     },
     
     methods: {
         createChart() {
             this.generateYLabels();
             this.generateDataset();
         },
         
         generateYLabels() {
             // generate an array of labels ['0h', '1h', '2h', ...]
             var array = [...Array(24).keys()];
             this.data[0].y = array.map(x => x + 'h');
         },
         
         generateDataset() {
             // generate an array of 24 arrays of random numbers
             var datasets = [];
             for (var i = 0; i < 24; i++) {
                 // generate an array of 7 random numbers
                 var dayPopulation = Array(7).fill(0).map(_ => Math.floor(Math.random() * 100));
                 datasets.push(dayPopulation);
             }
             this.data[0].z = datasets;
         },
     }
 }
</script>

<style>
 #app {
     font-family: 'Avenir', Helvetica, Arial, sans-serif;
     -webkit-font-smoothing: antialiased;
     -moz-osx-font-smoothing: grayscale;
     text-align: center;
     color: #2c3e50;
     margin-top: 60px;
 }

 h1, h2 {
     font-weight: normal;
 }

 ul {
     list-style-type: none;
     padding: 0;
 }

 li {
     display: inline-block;
     margin: 0 10px;
 }

 a {
     color: #42b983;
 }
 
 button {
     background-color: #4CAF50; /* Green */
     border: none;
     color: white;
     padding: 15px 32px;
     text-align: center;
     text-decoration: none;
     display: inline-block;
     font-size: 16px;
 }
</style>
