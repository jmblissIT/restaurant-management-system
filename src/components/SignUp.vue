<template>
  <img alt="Vue logo" src="../assets/logo.png">
<h1>Sign Up</h1>
<div>
    <input type="text" v-model="name" placeholder="Enter Name" />
    <input type="email" v-model="email" placeholder="Enter Email" />
    <input type="password" v-model="password" placeholder="Enter Password" />
    <button v-on:click="signUp">Sign Up</button>
    <p>
        <router-link to="/login">Login</router-link>
    </p>
</div>
</template>

<script>
/* eslint-disable vue/no-unused-components */
import axios from 'axios';
export default {
    name: 'SignUp',
    data()
    {
        return {
            name:'',
            email:'',
            password:''
        }
    },
    methods: {
        async signUp()
        {
            let result = await axios.post("http://localhost:3000/user", {
                email: this.email,
                password: this.password,
                name: this.name
            });

            console.warn(result);
            if(result.status==201)
            {
                //alert("sign-Up-Done");
                localStorage.setItem("user-info",JSON.stringify(result.data))
                this.$router.push({name:'Home'})
            }
        }
    },
    mounted()
    {
        let user = localStorage.getItem('user-info');
        if(user)
        {
            this.$router.push({name: 'Home'});
        }
    }
}
</script>