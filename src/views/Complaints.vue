<template>
<div class="dashboard">
    <navbar/>
    <v-form>
      <v-container fluid>
        <v-row>
          <v-layout row wrap >
            <v-flex xs10 md3>
              <v-col cols="12" sm="4">
                <v-text-field
                  :rules="rules"
                  counter="25"
                  label="Level 1 Code"
                  outlined
                ></v-text-field>
            </v-col>
            </v-flex>
              <v-btn class="mx-2" fab dark large color="cyan">
                  Search
               </v-btn>
               <v-spacer></v-spacer>
                <v-flex xs10 md3>
              <v-col cols="12" sm="4">
                <v-text-field
                  :rules="rules"
                  counter="25"
                  label="User Code"
                  outlined
                ></v-text-field>
            </v-col>
            </v-flex>
              <v-btn class="mx-2" fab dark large color="cyan">
                  Search
               </v-btn>
          </v-layout>    
        </v-row>
      </v-container>
    </v-form>
   <v-container fluid>
     <v-layout row class="mb-2">
       <v-tooltip top>
         <v-btn small flat class="primary" @click="sortBy('title')" slot="activator">
         <v-icon left small >folder</v-icon>
         <span class="caption text-lowercase">By Complaint</span>
        </v-btn>
        <span class="white--text">sort product by Complaint</span>
       </v-tooltip>
       <v-tooltip top>
          <v-btn small flat class="primary" @click="sortBy('status')" slot="activator">
         <v-icon left small >person</v-icon>
          <span class="caption text-lowercase">By status</span>
        </v-btn>
        <span class="white--text">sort by status</span>
       </v-tooltip>

     </v-layout>
     <v-card  class="white"  v-for="project in projects" :key="project.complaints_refn0">
       <v-layout row wrap :class="`pa-3 project ${project.status}`">
         <v-flex xs12 md4>
           <div class="caption grey--text">Complaint Category</div>
           <div>{{project.nature_complaint}}</div>  
         </v-flex>
         <v-flex xs6 sm4 md2>
           <div class="caption grey--text">Ref Number</div>
           <div>{{project.complaints_refn0}}</div>
         </v-flex>
         <v-flex xs6 sm4 md2>
           <div class="caption grey--text">Agent Name</div>
           <div>{{project.agent_name}}</div>
         </v-flex>
         <v-flex xs6 sm4 md2>
           <div class="caption grey--text">Date</div>
           <div>{{project.date}}</div>
         </v-flex>
         
         <v-flex xs2 sm4 md1>
          <div class="right">
            <v-chip  small :class="`${project.status}  white--text caption my-2`">
              {{project.status}}
            </v-chip>
          </div>
         </v-flex>
         <v-flex xs2 sm4 md1>
           <router-link   :to="{ name: 'Stepperview',
            params: { userData:{complaint:project.nature_complaint,refnumber:project.complaints_refn0,agentname:project.agent_name,
            date:project.date,phoneno:project.agent_phone,location:project.district,
            complaint_detail:project.complaint,levels:project.agent_staff,post:project.agent_staff,picto:project.picture} } }" >
				    <v-btn
                :color="getColor(project.status)"
                dark
                small
                class="mx-2"
              >
              <div class="mx-2">Reslove</div>
              </v-btn>
				</router-link>
         </v-flex>
       </v-layout>
       <v-divider></v-divider>
     </v-card>
     <!-- <div class="text-center">
    <v-pagination v-model="pagination.page" :length="pages"></v-pagination>
  </div> -->
  </v-container>
</div>
</template>

<script>
import navbar from '../components/DashViews/NavBar'
import axios from 'axios'
export default{
    components:{
      navbar
    },
  data(){
    return{
      
     e1: 0,
    // pagination: {
      
    // },
    
      projects:[],
      dialog: false,
      token: localStorage.getItem('token'),
      district_no: localStorage.getItem('district'),
      
      
     
    }
   
  },
   computed: {
    pages () {
      return this.pagination.rowsPerPage ? Math.ceil(this.items.length / this.pagination.rowsPerPage) : 0
    }
  },
  created(){
    axios.post('https://aaomach.pythonanywhere.com/getcomplaints',{'district_n0': this.district_no},
    {headers:{'x-access-token':this.token}}
    ).then(
      response => {this.projects = response.data})
  },

  methods: {
    sortBy(prop){
      this.projects.sort((a,b) => a[prop] < b[prop] ? -1:1)

    },
    getColor (status) {
        if (status =="Resolved" ) return 'orange'
        else if (status=="Declined") return 'red'
        else if (status=="Unresolved") return 'purple'
        else return 'green darken-2'
      }
        
      },
   
   
    

  }
 



</script>
<style lang="stylus" scoped>
.project.Pending{
  border-left: 4px solid green
}
.project.Resolved{
  border-left: 4px solid orange
}
.project.Declined{
  border-left: 4px solid tomato
}
.project.Unresolved{
  border-left: 4px solid purple
}
.v-chip.Pending{
  background: green 
}
.v-chip.Resolved{
  background:  #004080
}
.v-chip.Declined{
  background:  tomato
}
.v-chip.Unresolved{
  background:  purple
}
</style>
