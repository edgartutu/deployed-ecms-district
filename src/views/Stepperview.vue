<template>
<div>
  <navbar/>
  <v-stepper v-model="e1">
    <v-stepper-header class="purple" >
      <v-stepper-step class="white--text"  :complete="e1 > 1" step="1">Complaint Details</v-stepper-step>
      <v-divider></v-divider>
      <v-stepper-step :complete="e1 > 2" step="2">Complaint Resolution</v-stepper-step>
      <v-divider></v-divider>
      <v-stepper-step step="3">View</v-stepper-step>
    </v-stepper-header>
    <v-stepper-items>
      <v-stepper-content  step="1">
        <v-container>
          <v-layout  >
            <v-flex
              xs12
              md12  
            >
            <v-card
          class="mb-12"
          flat
          >
          <v-container>
              <v-layout row wrap>
                  <v-flex xs12 md4>
                        <div class=" green--text">Complainant</div>
                        <p>{{userData.agentname}}</p>
                  </v-flex>
                  <!-- <v-flex xs12 md2>
                        <div class=" green--text">Level</div>
                        <p>{{userData.levels}}</p>
                  </v-flex> -->
                   <v-flex xs12 md2>
                       <div class=" green--text">Position Held</div>
                         <p>{{userData.post}}</p>
                  </v-flex>
                  <v-flex xs12 md2>
                        <div class=" green--text">Phone Number</div>
                        <p>{{userData.phoneno}}</p>
                  </v-flex>
                  <v-flex xs12 md2>
                         <div class=" green--text">Location</div>
                         <p>{{userData.location}}</p>
                  </v-flex>
              </v-layout >
                <div class="red--text">Ref Number</div>
               <p>{{userData.refnumber}}</p>
                <div class=" green--text">Complaint Category</div>
               <p>{{userData.complaint}}</p>
                <div class=" green--text">Complaint Details</div>
               <p>{{userData.complaint_detail}}</p>
               
                <div class="green--text">Date</div>
               <p>{{userData.date}}</p>
               </v-container>
               </v-card>
            </v-flex>
          </v-layout>
        </v-container>
        <unresolve/>
         <decline/>
        <v-btn
        class="right"
          color="primary"
          @click="e1 = 2"
          small
          tile 
          outlined
        >
          Continue
        </v-btn>
      </v-stepper-content>

      <v-stepper-content step="2">
       
        <v-container>
          <v-layout  >
            <v-flex
              xs12
              md12  
            >
            <v-card
          class="mb-12"
          flat
          >
          <v-container>
              <v-layout row wrap>
                <v-spacer></v-spacer>
                  <v-flex xs4 md4>
                         <!-- <v-dialog
                    v-model="dialog"
                    width="500"
                  >
                    <template v-slot:activator="{ on }">
                      <v-btn
                        color="blue-grey darken-1"
                        dark
                        v-on="on"
                        class="right"
                        :disabled='isDisable(userData.resolving,userData.distro)'
                        
                      >
                        Amend Resolution
                      </v-btn>
                    </template>

                    <v-card>
                      <v-card-text>
                        <v-container>
                            <v-layout row wrap>
                                <v-flex xs12 md12>
                                      <v-textarea :rules="nameRules" label="Description" v-model="classify" required ></v-textarea>
                                </v-flex>
                            </v-layout >
                            </v-container>
                      </v-card-text>
                      <v-divider></v-divider>
                      <v-card-actions>
                        <div class="flex-grow-1"></div>
                        <router-link to="/projects">
                          <v-btn
                          color="primary"
                          text
                         @click="dialog = false;submis()"
                         :disabled='isDisable(userData.resolving,userData.distro)'
                          >
                          Amend
                        </v-btn>
                        </router-link>
                        
                      </v-card-actions>
                    </v-card>
                  </v-dialog> -->
                  </v-flex>
                  <!-- <v-flex xs12 md6>
                        <v-text-field :rules="nameRules"  label="NiN Number" required v-model="nin"></v-text-field>
                  </v-flex> -->
                  <!-- <v-flex xs12 md12>
                        <v-text-field :rules="nameRules"  label="Complaint Clasification" required v-model="classification"></v-text-field>
                  </v-flex> -->
                  <v-flex xs12 md12>
                        <v-textarea :rules="nameRules" label="Complaint Resolution" required v-model="resolution"></v-textarea>
                  </v-flex>
                  <v-flex xs12 md12>
                        <v-textarea :rules="nameRules" label="Remarks" required v-model="details"></v-textarea>
                  </v-flex>
                  <v-flex xs6 md6>
                         <v-col cols="12" sm="6">
                            <v-text-field label="Signatue(Your name)" single-line outlined :rules="nameRules" required v-model="signature"></v-text-field>
                        </v-col>
                  </v-flex>
                 
              </v-layout >
               </v-container>
               </v-card>
            </v-flex>
          </v-layout>
        </v-container>
        <v-btn
          class="left"
          color="primary"
          @click="e1 = 1"
          small
          tile 
          outlined
        >
          Back
        </v-btn>
        <router-link to="/projects">
             <v-btn
          :disabled='isDisabled(userData.resolving,userData.distro)'
          color="green darken-4"
          @click="e1 = 3;submit()"
          
        >
          Submit
        </v-btn>
        </router-link>
        <v-btn class="right"
          color="primary"
          @click="e1 = 3"
          small
          tile 
          outlined
        >
          Continue
        </v-btn>

      </v-stepper-content>
        
      <v-stepper-content step="3">
        <v-container>
          <v-layout>
            <v-flex xs12 md12>
                    <v-card id="print"   class="mb-12"  flat >
                      <v-avatar size="100">
                        <img
                            src="@/assets/img/com.jpg"
                            alt="John"
                          
                        >
                        </v-avatar>
                        <h3>Orgainsation Name</h3>
                        <h3 style="color: #004080;" class="font-weight-bold">Certificate Of Resolution</h3>
                        <h4 class="red--text" style="font-weight:bold;">{{userData.refnumber}}</h4>
                        <h4 class="font-weight-bold">Complaint</h4>
                        <p>{{userData.complaint_detail}}</p>
                        <h4 class="font-weight-bold" >District Resolution :</h4>
                        <p>{{userData.distro}}</p>
                        <!-- {{userData}} -->
                        <h4 class="font-weight-bold" >HeadQuater Resolution :</h4>
                        <p>{{userData.resolving}}</p>
                         <h4 class="font-weight-bold" >Remarks:</h4>
                        <p>{{userData.dis}}</p> <p>{{userData.remaks}}</p>
                         <!-- <h4 class="font-weight-bold" >Amendment</h4>
                        <p>{{userData.classify}}</p> -->
                        
                        <div class="left " >ReportDate:  {{userData.date}}  </div><br>
                        <div class="left">ResolvedDate: {{userData.dt}}</div>
                        <div class="right">signature: ...........................................</div>
                        <br>
                        <div class="right">District Returning Officer</div>
                    </v-card>
            </v-flex>
          </v-layout>
        </v-container>
         <v-btn
          class="left"
          color="primary"
          @click="e1 = 2"
          small
          tile 
          outlined
        >
          Previous
        </v-btn>
        <v-btn
        class="right"
          color="teal"
          @click.native="print"
        >
          Print
        </v-btn>
      </v-stepper-content>
    </v-stepper-items>
  </v-stepper>
  </div>
</template>
<script>
import axios from 'axios'
import data1 from '@/views/Complaints.vue'
import decline from '../components/DashViews/Decline.vue'
import unresolve from '../components/DashViews/Unresolved.vue'
  import router from '../router'
  import navbar from '../components/DashViews/NavBar'
  export default {
      name:'Stepperview',
    components:{
      data1,
      decline,
      navbar,
      unresolve
    },
    data () {
      return {
        terms: false,
        e1: 0,
        post:"None",
        dialog: false,
        nin:"None",
        classification:"None",
        resolution:"",
        details:"",
        signature:"",
        classify:"",
        userData: 0,
        debug: false,
        nameRules: [
        v => !!v || 'Input is required',
        // v => (v && v.length <= 10) || 'Name must be less than 10 characters',
      ],
      email: localStorage.getItem('user'),
      token: localStorage.getItem('token')
      
      }
    },
    created() {
            this.userData = this.$route.params.userData;
        },
        computed: {
  
},

    methods:{
         
       isDisable(resolving,distro){
      if(resolving &&!distro)
      return !this.terms
      else if (!resolving &&!distro)
      return !this.terms
      else return this.terms
    },
       isDisabled(resolving,distro){
      if(resolving || distro)
      return !this.terms
      else return this.terms
    },
      submit(){
        axios.post('https://aaomach.pythonanywhere.com/postcomplaints',{
          'status':'Resolved','complaints_refn0':this.userData.refnumber, 'admin_email':this.email,
          'districtagent_idn0':this.nin,'districtagent_post':this.post,
          'district_resolutions':this.resolution,'classify_complaint':this.classification,
          'district_description':this.details
          },
          {
            headers:{
            'x-access-token':this.token
            }
        })
          // console.log(this.userData.refnumber)
      },
       submis(){
        axios.post('https://aaomach.pythonanywhere.com/AmendComplaints',{
          'status':'Resolved','complaints_refn0':this.userData.refnumber, 'admin_email':this.email,
          
         'classify_complaint':this.classify,
        
          },
          {
            headers:{
            'x-access-token':this.token
            }
        })
          // console.log(this.userData.refnumber)
      },
       print(){
        // Get HTML to print from element
const prtHtml = document.getElementById('print').innerHTML;

// Get all stylesheets HTML
let stylesHtml = '';
for (const node of [...document.querySelectorAll('link[rel="stylesheet"], style')]) {
  stylesHtml += node.outerHTML;
}

// Open the print window
const WinPrint = window.open('', '', 'left=0,top=0,width=800,height=900,toolbar=0,scrollbars=0,status=0');

WinPrint.document.write(`<!DOCTYPE html>
<html>
  <head>
    ${stylesHtml}
  </head>
  <body>
  <img
  src="@/assets/img/com.jpg"
  alt="John"
id="print"  
>
${prtHtml}
  </body>
</html>`);

WinPrint.document.close();
WinPrint.focus();
WinPrint.print();
// WinPrint.close();
      }
    }
    
  }
</script>