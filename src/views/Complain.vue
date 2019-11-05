<template>
<div class="dashboard">
    <navbar/>
    <v-layout wrap >
    <h2 class="purple--text">Complaint Form</h2>
         <v-flex xs12 md12>
            <v-card  class="white "  >
              <v-container fluid >
              <!-- <v-flex xs12 md6>
                  <v-text-field v-model="district"   label="District code" required ></v-text-field>
              </v-flex> -->
                <v-flex xs12 md6>
                  <v-text-field v-model="town"  label="Town" required ></v-text-field>
              </v-flex>
              <v-flex xs12 md12>
                  <v-select
                      v-model="select"
                      :items="itemz"
                      label="Position"
                      required
                    ></v-select>
              </v-flex>
              
                <v-flex xs12 md12>
                  <v-select
                  v-model="select2"
                  :items="items"
                  label="Classification"
                   required
                    ></v-select>
              </v-flex>
              
                <v-flex xs12 md12>
                  
                  <v-textarea
                    v-model="complaints"
                    counter
                    label="Complaint"
                    :rules="rules"
                    
                  ></v-textarea>
              </v-flex>
            </v-container>
            <router-link to="/team">
                <v-btn flat class="green" @click="submit()" >Submit</v-btn>
            </router-link>
            </v-card>
         </v-flex>
       </v-layout>
  
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
        town:'',
        select:'',
        select2:'',
        complaints:'',
        // district:'',
        rules: [v => v.length <= 500 || 'Max 500 characters'],
      items: [
        'Registration/Update',
        'Display/Register',
        'Nomination',
        'Campaigns',
        'Polling Day',
        'General Complaint'
      ],
      itemz:[
        'Staff',
        'Non Staff'
      ],
       
       radios: 'radio-1',
      projects:[],
      dialog: false,
    
      token: localStorage.getItem('token')
      
     
    }
   
  },
   computed: {
    pages () {
      return this.pagination.rowsPerPage ? Math.ceil(this.items.length / this.pagination.rowsPerPage) : 0
    }
  },
  

  methods: {
   
    getColor (status) {
        if (status =="Resolved" ) return 'orange'
        else if (status=="Declined") return 'red'
        else if (status=="Unresolved") return 'purple'
        else return 'green darken-2'
      },
      submit(){
        axios.post('https://aaomach.pythonanywhere.com/postadmin1Complaint',{'email':localStorage.getItem('user'),'agent_staff':this.select,
     'district':localStorage.getItem('district'),'poling_station':this.town,'nature_complaint':this.select2,'complaint':this.complaints},
     {
       headers:{
       'x-access-token':this.token
     }
     }
     ).then(response=>{
                window.location.reload()
            })
      }
        
      },
   
   
    

  }
 



</script>
<style lang="scoped">
/* .custom-selector{
  font-size: 3em;
  
} */
</style>
