<template>
        <v-row
          align="center"
          justify="center"
        >
          <v-col
            cols="6"
            sm="8"
            md="4"
          >
          <v-layout row justify-center>
            <v-flex sm12 md6>
                 <v-card class="elevation-12" >
              <v-toolbar
                color="#5e0c1d"
                dark
                flat
              >
                <v-toolbar-title class="white--text">Register form</v-toolbar-title>
                <div class="flex-grow-4"></div>
               <h2 style="margin-left:30%;" class="purple--text">eCMS</h2>
                <v-spacer></v-spacer>
                <!-- <v-tooltip right> -->
                  <!-- <template v-slot:activator="{ on }"> -->
                      <router-link to="/login">
                            <v-btn
                            icon
                            large
                            href="https://codepen.io/johnjleider/pen/pMvGQO"
                            target="_blank"
                            v-on="on"
                            >
                            Login
                            </v-btn>
                      </router-link>
                  <!-- </template> -->
                  <!-- <span class="white--text" >Login Now</span> -->
                <!-- </v-tooltip> -->
              </v-toolbar>
              <v-card-text>
                <v-form>
                  <v-text-field
                    label="Name"
                    v-model="name"
                    name="login"
                    prepend-icon="person"
                     :rules="[() => !!name || 'This field is required']"
                    type="text"
                  ></v-text-field>

                  <v-text-field
                    label="Email"
                    v-model="email"
                    name="login"
                    prepend-icon="email"
                     :rules="[() => !!email || 'This field is required']"
                    type="text"
                  ></v-text-field>
                  <v-text-field
                    label="Tel"
                    v-model="tel"
                    name="login"
                    prepend-icon="email"
                     :rules="[() => !!tel || 'This field is required']"
                    type="text"
                  ></v-text-field>
                  <v-text-field
                    label="Post"
                    v-model="post"
                    name="post"
                    prepend-icon="email"
                     :rules="[() => !!post || 'This field is required']"
                    type="text"
                  ></v-text-field>
                  <v-text-field
                    label="District"
                    v-model="district"
                    name="district"
                    prepend-icon="email"
                     :rules="[() => !!district || 'This field is required']"
                    type="text"
                  ></v-text-field>
                  <v-text-field
                    id="password"
                    label="Password"
                    v-model="password"
                    name="password"
                     :rules="[() => !!password || 'This field is required']"
                    prepend-icon="lock"
                    type="password"
                  ></v-text-field>
                  <v-text-field
                    id="confirm"
                    label="Confirm Password"
                    v-model="confirm"
                    name="password"
                     :rules="[() => !!confirm || 'This field is required']"
                    prepend-icon="lock"
                    type="password"
                  ></v-text-field>
                </v-form>
              </v-card-text>
              <v-card-actions>
                <div class="flex-grow-1"></div>
                <v-btn color="primary" @click="submit()">Register</v-btn>
              </v-card-actions>
            </v-card>
            </v-flex>
          </v-layout>
           
           
          </v-col>
        </v-row>
</template>
<script>
import axios from 'axios'
  export default {
    props: {
      source: String,
    },
    data() {
      return {
        drawer: null,
        name:'',
        email:'',
        tel:'',
        post:'',
        password:'',
        confirm:'',
        district:'',
      }
      
    },
    methods:{
      submit(){
        //console.log('hello')
        axios.post('https://aaomach.pythonanywhere.com/register',{
          'Name':this.name,'email':this.email,'post':this.post,'district':this.district,'tel':this.tel,'password':this.password,'confirm_password':this.confirm
          }).then(response=>{
                window.location.reload()
            })
      }
    }
  }
</script>