<template>
    <nav>
       <v-toolbar style=" background-color: #5e0c1d;" app fixed>
           <v-toolbar-title class="purple--text" >eCMS</v-toolbar-title>
           <p></p>
           <p></p>
            <v-toolbar-items class="hidden-sm-and-down" >
                <v-layout  row >
                <v-btn  flat small  class=" mx-2 white--text" v-for="link in links" :key="link.text" router :to="link.route">
                    <span>{{link.text}}</span>
                </v-btn>
                </v-layout>
            </v-toolbar-items>
            <v-spacer></v-spacer>
                <p></p>
                 <v-menu class="hidden-md-and-up">
                    <v-toolbar-side-icon slot="activator" class="purple--text"   ></v-toolbar-side-icon>
                    <v-list>
                    <v-list-tile v-for="link in links" :key="link.text" router :to="link.route">
                        <v-list-tile-content>
                        <v-list-tile-title class="purple--text">{{ link.text}}</v-list-tile-title>
                        </v-list-tile-content>
                    </v-list-tile>   
                    </v-list>
                </v-menu>
                <router-link v-ripple  to="/dashboard">
					<v-icon class="mx-2" color>mdi-home</v-icon><br>
				</router-link>
                <v-menu bottom left content-class offset-y transition="slide-y-transition">
					<router-link v-ripple slot="activator"  to="/projects">
						<v-badge class="#E65100" overlap>
					        <template slot="badge">{{projects.length}}</template>
					            <v-icon class="mx-2" color>mdi-bell</v-icon>
				        </v-badge>
					</router-link>
					<v-card>
						<!-- <v-list dense>
							<v-list-tile v-for="notification in notifications" :key="notification" @click="onClick">
								<v-list-tile-title v-text="notification"/>
							</v-list-tile>
						</v-list> -->
					</v-card>
				</v-menu>
                     <v-btn flat class="white--text" @click="logout()">
                    <span>SignOut</span>
                    <v-icon>exit_to_app</v-icon>
                    </v-btn> 
        </v-toolbar>
    </nav>
</template>
<script>
	
import axios from 'axios'
export default {
    data(){
        return{
            links:[
                { text:'Dashboard', route:'/dashboard'},
                { text:'Complaints', route:'/projects'},
                { text:'Registry',route:'/team'},
                 { text:'Stores',route:'/store'},
            ],
            projects:[
      
      ],
      district: localStorage.getItem('district'),
      token: localStorage.getItem('token')
        }
    },
      created(){
           axios.post('https://aaomach.pythonanywhere.com/Pendings',{'district_n0':this.district}).then(
        response =>{
          this.projects = response.data
           
        }
      )
  },
  methods:{
        logout() {
				this.$store.dispatch("logout").then(() => {
					this.$router.push("/");
				});
			}
      
      }
       
    

}
</script>

