<template>
    <img class="logo" src="../assets/M.jpg.avif" />
    <h1>Sign Up</h1>
    <div class="register">
        <input type="text" v-model="name" placeholder="Enter Name"/>
        <input type="email" v-model="email" placeholder="Enter Email"/>
        <input type="password" v-model="password" placeholder="Enter Password"/>
        <button v-on:click="signUp">Sign Up</button>
        <p>
            <router-link to="./login">Login</router-link>
        </p>
    </div>
</template>

<script>
import axios from 'axios'
export default {
    name:'SignUp',
    data()
    {
        return {
            name:'',
            email:'',
            password:''
        }
    },
    methods:{
        async signUp()
        {
            let result = await axios.post("http://localhost:3000/user",{
                name:this.name,
                email:this.email,
                password:this.password
            });
            console.warn(result);
            if(result.status==201)
            {
                localStorage.setItem("user-info", JSON.stringify(result.data))
                this.$router.push({name:'Home'})
            }
        }
    },
    mounted()
    {
        let user = localStorage.getItem("user-info");
        if(user)
        {
            this.$router.push({name:'Home'})
        }
    }
}
</script>

<style>
.logo{
    width: 200px;
    padding-top: 10px;
    border-radius: 10%;
}
.register input, .add input{
    width: 300px;
    height: 40px;
    padding-left: 20px;
    display: block;
    margin-bottom: 30px;
    margin-right: auto;
    margin-left: auto;
    border: 1px solid goldenrod;
}
.register button, .add button{
    background-color: goldenrod;
    border: 1px solid goldenrod;
    color: aliceblue;
    cursor: pointer;
}
</style>