<template>
<div >
 
   <v-container max-height="400px" style="overflow-y: auto">
     <v-card  flat class="white"  v-for="project in projects" :key="project.content">
       <v-layout row wrap :class="`pa-3 project ${project.status}`">
         <v-flex xs12 md6>
           <div class="caption grey--text">Complaint Category</div>
           <div>{{project.nature_complaint}}</div>  
         </v-flex>
         <v-flex xs4  md6>
          <div class="right">
            <v-chip  small :class="`${project.status} white--text caption my-3`">
              {{project.status}}
            </v-chip>
          </div>
         </v-flex>
       </v-layout>
        
     </v-card>
     
  </v-container>
</div>
 
</template>

<script>
import axios from 'axios'
export default{

  data(){
    return{
      projects:[],
      district: localStorage.getItem('district'),
      token: localStorage.getItem('token')

      
    }
  },
  created(){
    axios.post('https://aaomach.pythonanywhere.com/getcomplaints',{'district_n0':this.district},
    {
       headers:{
       'x-access-token':this.token
     }
     }
    
    ).then(response =>{
      this.projects = response.data
    }
      
    )
  }
  

}

</script>

<style lang="stylus" scoped>
.project.Pending{
  border-left: 4px solid #5e0c1d;
}
.project.Resolved{
  border-left: 4px solid #004080;
}
.project.Declined{
  border-left: 4px solid tomato;
}
.v-chip.Pending{
  background: green;
}
.v-chip.Resolved{
  background:  #004080;
}
.v-chip.Declined{
  background:  tomato;
}
.v-chip.Unresolved{
    background: #5e0c1d;
}

</style>
