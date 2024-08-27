<template>
    <img class=logo src="../assets/Starbucks.svg.png" />
    <h1>Sign Up</h1>
    <div class="register">
        <input type="text" v-model="name" placeholder="Enter Name" />
        <input type="text" v-model="email" placeholder="Enter Email" />
        <input type="password" v-model="password" placeholder="Enter Password" />
        <button v-on:click="passUp">Sign Up</button>
    </div>
</template>

<script>
import axios from 'axios'
export default{
    name:'SignU',
    data(){
        return{
            name:'',
            email:'',
            password:''
        }
    },
    methods:{
        async passUp()
        {
            let result = await axios.post("http://localhost:3000/user",{
                name:this.name,
                email:this.email,
                password:this.password
            });
            console.warn(result);
            if(result.status==201)
            {
                alert("signup dah woi")
                localStorage.setItem("set-info", JSON.stringify(result.data))
            }
        }
    }
}
</script>

<style>
.logo{
    width: 100px;
}
.register input{
    width: 300px;
    height: 40px;
    padding-left: 20px;
    display: block;
    margin-bottom: 30px;
    margin-left: auto;
    margin-right: auto;
    border: 1px solid green;
}
.register button{
    background-color: green;
    border: 1px solid green;
    color: aliceblue;
    cursor: pointer;
}
</style>