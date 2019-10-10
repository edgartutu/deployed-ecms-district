<template>
<div class="dashboard">
  <navbar/>
 
   <v-layout row wrap justify-space-around>
     <v-flex xs10 md5>
       <v-card class="pa-3" outline  max-width="800" height="400px">
         <pie/>
       </v-card>
     </v-flex>
     <v-flex xs10 md5>
       <v-card class="pa-2" outline max-width="800"  height="400px"> 
         <div width="1000px"><bar/></div>
         
       </v-card>
     </v-flex>
   </v-layout><br>
   <v-layout row wrap justify-space-around>
     <v-flex xs10 md5>
       <v-card class="pa-3" outline max-width="800"  height="400px">
         <donut/>
       </v-card>
     </v-flex>
     <v-flex xs10 md5 >
       <v-card max-height="400px" style="overflow-y: auto" class="pa-3" outline max-width="800"  height="400px">
         <carlender/>
       </v-card>
     </v-flex>
   </v-layout>
   

 
</div>
 
</template>

<script>
import axios from 'axios'
import pie from '../components/DashViews/PieChart.vue'
import donut from '../components/DashViews/Donut.vue';
import bar from '../components/DashViews/BarChart.vue'
import carlender from '../components/DashViews/Carlender.vue'
import navbar from '../components/DashViews/NavBar'

export default{
    components:{
      pie,
      donut,
      bar,
      carlender,
      navbar
    },
  data(){
    return{
     
      
    }
  },

}

</script>