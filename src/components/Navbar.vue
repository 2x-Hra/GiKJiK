<template>
    <div class="navbar">
        <v-snackbar v-model="snackbar" :timeout="4000" top color="success">
            <span>Awesome! you added new class.</span>
            <v-btn text color="white" @click="snackbar = false">Close</v-btn>
        </v-snackbar>
        <v-toolbar flat class="teal lighten-5" >
            <!-- <v-app-bar-nav-icon color="teal accent-4" @click="drawer = !drawer"></v-app-bar-nav-icon> -->
            
            <v-toolbar-title class="text-uppercase " >
                <span class="font-weight-light " style="color:#00BFA5;" >GiK</span>
                <span  style="color:#00BFA5;">JiK</span>
            </v-toolbar-title>

            <v-spacer></v-spacer>
            <v-row>
                <v-col cols="12" sm="3">
                    
                </v-col>  
                <v-col cols="12" sm="3">
                    
                </v-col> 
                <v-col cols="12" sm="6">
                    <!-- <v-text-field outlined label="Search Class" solo  rounded  dense  append-icon="search"  class="mt-6" >

                    </v-text-field> -->
                </v-col> 
                    
                
                   
            
                
            </v-row>
                
            <v-menu offset-y>
                <template v-slot:activator="{ on }">
                    <v-btn text v-on="on" color="teal accent-4">
                        <v-icon left>expand_more</v-icon>
                        <span>Menu</span>
                    </v-btn>
                </template>
                
                <v-list>
                    <v-list-item v-for="link in links" :key="link.text" router :to="link.route">
                        <v-list-item-title>{{ link.text }}</v-list-item-title>
                    </v-list-item>
                </v-list>
            </v-menu>

            <v-btn @click="move" rounded text color="teal accent-4">
                <span>Sign Out</span>
                <v-icon right>exit_to_app</v-icon>

            </v-btn>
        </v-toolbar>
        <v-navigation-drawer app 
            class="teal accent-5"
            color="teal"
            v-model="drawer"
            bottom
            
                >
                <v-layout column align-center>
                    <v-flex class="mt-8 mb-5">
                        <v-avatar size="100">
                            <img src="/avatar-1.png" alt="">
                        </v-avatar>
                        <p class="white--text subtitle-1 mt-3" align="center">
                            {{username}}
                        </p>
                    </v-flex>

                    <v-flex mb-5>
                        <app-Create-Class-Popup @projectAdded="snackbar=true"></app-Create-Class-Popup>
                    </v-flex>
                </v-layout>

            <v-list dense nav>
                <v-list-item  v-for="link in links" :key="link.text" router :to="link.route">
                    <v-list-item-action>
                        <v-icon class="white--text">{{ link.icon }}</v-icon>
                    </v-list-item-action>
                    <v-list-item-content>
                        <v-list-item-title class="white--text">
                            {{ link.text }}
                        </v-list-item-title>
                    </v-list-item-content>
                </v-list-item>
            </v-list>
        </v-navigation-drawer>
    </div>
</template>

<script>
    import axios from 'axios'
    import CreateClassPopup from './CreateClassPopup'
    export default {
        components:{
            appCreateClassPopup :CreateClassPopup
        },
        data() {
            return {
                username:'',

                drawer: true,
                links: [
                    { icon: 'home', text: 'Home', route: '/userHome'},
                    { icon: 'class', text: 'Class Manager', route: '/classmanagment'},
                    
                    
                ],
                snackbar:false
            }
        },
        methods:{
            move:function(){
                axios.defaults.headers.common['Authorization'] = " ";
                localStorage.clear();
                this.$router.push({name :'Entrance'})
            }
        },
        created(){
            axios.get('http://127.0.0.1:8000/username/retrieve/', { headers: { Authorization:localStorage.getItem('LearnOnlineToken') }})
            .then(response =>{
                this.username = response.data.username
                
            })
        }
        
    }
</script>