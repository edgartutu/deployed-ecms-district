<template>
  <div class="small">
    <bar-chart :chart-data="datacollection" height="390px"></bar-chart>
    <!-- <button @click="fillData()">Randomize</button> -->
    
    
    
  </div>
</template>

<script>
  import BarChart from '../BarChart.js';
  import axios from 'axios'

  export default {
    components: {
      BarChart
    },
    data () {
      return {
        datacollection: null,
        datas:null,
        datah:null,
        options:{
          xAxes: [{
            barPercentage: 0.5,
            barThickness: 30,
            maxBarThickness: 8,
            minBarLength: 2,
            gridLines: {
                offsetGridLines: true
            }
        }]
        }

      }
    },
    created(){
        axios.post('https://aaomach.pythonanywhere.com/Monthly',{"district_n0":localStorage.getItem('district')}).then(
      response => {this.datas = response.data.dema
                    this.datah = response.data.deta
                   
                console.log(this.datah)
      })
      
    },
    mounted () {
      this.fillData()
    },
    methods: {
      fillData () {

        
        
        this.datacollection = {
          labels: ['January', 'February', 'March', 'April', 'May', 'June', 'July', 'August', 'September', 'October', 'November', 'December'],
          datasets: [
            {
              label: 'Unresolved',
              backgroundColor: '#5e0c1d',
              datas: []
            }, {
              label: 'Resolved',
              backgroundColor: '#004080',
              data: []
            }
          ]
        }
      },

      
      getRandomInt () {
        return Math.floor(Math.random() * (50 - 5 + 1)) + 5
      }
    },
     watch:{
    datas(newData){
      const data =this.datacollection
      data.datasets[1].data=newData
      this.datacollection={...data}
    },
    datah(newData){
      const data =this.datacollection
      data.datasets[0].data=newData
      this.datacollection={...data}
    }
  },

  }
</script>

<style>
  .small {
    max-width: 400px;
    margin:  auto auto;
  }
</style>