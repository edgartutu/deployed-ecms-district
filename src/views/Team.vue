<template>
  <div>
    <navbar/>
    <!-- <div class="text-center"> -->
     
    <!-- </div>  -->
    <v-container fluid>
  <v-layout row wrap column>       
    <v-flex xs12 md12 >
       <export-excel style="float:left;" :data="items">
            <h6  >Export to Excel</h6>
            <img src="@/assets/img/512.png" style="width:40px;height:40px">
        </export-excel> 
        <v-flex>
          <router-link to="/report">
              <v-btn style="float:right;" ripple outlined color="indigo">Register Complaint</v-btn>
          </router-link>
        </v-flex>
        
      <v-text-field
            v-model="search"
            append-icon="search"
            label="Search"
            single-line
            hide-details
          ></v-text-field>
        <v-data-table class="fb-table-elem"
            :headers="headers"
            :items="items"
             :search="search"
            hide-actions
            item-key="name"
            expand >
            <template slot="items" slot-scope="props" >          
              <tr @click="props.expanded = !props.expanded">  
                <td class="datatable-cell-wrapper"><div>{{ props.item.nature_complaint }}</div></td>
                <td class="datatable-cell-wrapper"><div>{{ props.item.complaints_refn0}}</div></td>
                <!-- <td class="datatable-cell-wrapper">{{ props.item.complaint }}</td> -->
                <td class="datatable-cell-wrapper">{{ props.item.district }}</td>
                <td class="datatable-cell-wrapper">{{ props.item.date }}</td>
                <td class="datatable-cell-wrapper">{{ props.item.date_submit }}</td>
                
                <v-dialog
                v-model="dialog"
                width="600"
                >
                  <template v-slot:activator="{ on }">
                    <v-btn
                      small 
                      class="pink"
                      v-on="on"
                    >
                    review
                    </v-btn>
                      </template>
                        <v-card>
                            <v-card-title
                            class="purple"
                          primary-title
                          style="color:white;"
                            >
                            Complaint Details
                          </v-card-title>
                                <v-btn class="right teal"  @click.native="print">Print</v-btn>
                                   <v-card-text id="print" class="px-16">
                                     <v-avatar size="100">
                                      <img
                                          src="@/assets/img/com.jpg"
                                          alt="John"
                                          
                                      >
                                      </v-avatar>
                                      
                                      <h3>Orgainsation Name</h3>
                                      <h3 style="color: #004080;" class="font-weight-bold">Certificate Of Resolution</h3>
                                      <h4 class="red--text" style="font-weight:bold;">{{props.item.complaints_refn0}}</h4>
                                      <!-- <h4 class="font-weight-bold">Complaint Ref</h4>
                                      <p>{{props.item.complaints_refn0}}</p> -->
                                      <!-- <h4 class="font-weight-bold">Complaint Category</h4>
                                      <p>{{props.item.nature_complaint}}</p> -->
                                      <h4 class="font-weight-bold">Complainant</h4>
                                      <p>{{props.item.complaint}}</p>
                                      <!-- <h4 class="font-weight-bold">Location</h4>
                                      <p>{{props.item.district}}</p> -->
                                      <h4 class="font-weight-bold">District Resolution</h4>
                                      <p>{{props.item.district_resolutions}}</p>
                                       <h4 class="font-weight-bold">HeadQuater Resolution</h4>
                                      <p>{{props.item.headresolution}}</p>
                                       <h4 class="font-weight-bold">Remarks</h4>
                                      <p>{{props.item.district_description}}</p>
                                       <h4 class="font-weight-bold">Amendement</h4>
                                      <p>{{props.item.classify_complaint}}</p>
                                      <div class="left font-weight-bold">Date Recieved :</div>
                                      <div class="left">{{props.item.date}}</div><br>
                                        <div class="left font-weight-bold">Date Resolved :</div>
                                      <div class="left">{{props.item.date_submit}}</div> 
                                      <div class="right">Signature: ...........................................</div>
                                      <br>
                                      <div class="right">Director Technical And Support Services</div><br>
                                      
                                     
                                      
                                      
                                      
                                  </v-card-text> 
                            <v-divider></v-divider>
                            <v-card-actions>
                              <!-- <v-spacer></v-spacer> -->
                                <v-dialog
                                v-model="dialog"
                                width="200"
                                >
                                  <v-card>
                                    <v-card-text>
                                      <h4 style="color:green">Successfull</h4> 
                                    </v-card-text>
                                    <v-card-actions>
                                      <v-spacer></v-spacer>
                                      <v-spacer></v-spacer>
                                    </v-card-actions>
                                  </v-card>
                                </v-dialog>
                                <v-spacer></v-spacer>
                                <v-dialog
                                v-model="dialog"
                                width="200"
                                >
                                  <v-card>
                                    <v-card-text>
                                      <h4 style="color:red"> Rejected!</h4>
                                      </v-card-text>
                                      <v-card-actions>
                                        <v-spacer></v-spacer>
                                        </v-card-actions>
                                        </v-card>
                                        </v-dialog>
                            </v-card-actions>
                          </v-card>
                        </v-dialog>
                </tr>
              </template>
            </v-data-table>
      </v-flex>
      </v-layout>
      </v-container>
  </div>
</template>
<script>
import navbar from '../components/DashViews/NavBar'
import axios from 'axios'
  export default {
    components:{
      navbar
    },
    data(){
    
      return {
        search: '',
      headers: [
        { text: 'Complaint Category', value: 'nature_complaint' },
        { text: 'Complaint Ref', value: 'complaints_refn0' },
          // { text: 'Complainant', value: 'complaint' },
          { text: 'Location', value: 'district' },
          { text: 'Date Recieved', value: 'date' },
          { text: 'Date Resolved ', value: 'date_submit' },
      
      ],
      items: []
      
    }
    
    
    }, 
    created(){
      axios.post('https://aaomach.pythonanywhere.com/allcomplaints',{"district_n0":localStorage.getItem('district')}).then(
        response =>{
          this.items = response.data
        }
      )
    },
     methods:{
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
