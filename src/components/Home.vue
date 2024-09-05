<template>
    <Header />
    <h1>Hi {{name}}! Movie Library</h1>
    <table border="1" class="table">
        <tr>
            <td>Id</td>
            <td>Name</td>
            <td>Year Release</td>
            <td>Movie Rating</td>
            <td>Action</td>
        </tr>
        <tr v-for="item in movie" :key="item.id">
            <td>{{ item.id }}</td>
            <td>{{ item.name }}</td>
            <td>{{ item.release }}</td>
            <td>{{ item.rating }}</td>
            <td>
                <button class="update" v-on:click="goToUpdate(item.id)">Update</button>
                <button class="deletebutton" v-on:click="deleteMovie(item.id)">Delete</button>
            </td>
        </tr>
    </table>
</template>

<script>
import axios from 'axios';
import Header from './Header.vue'
export default{
    name:'Home',
    data(){
        return{
            name:'',
            movie:[],
        }
    },
    components:{
        Header
    },
    methods:{
        async deleteMovie(id)
        {
            let result=await axios.delete("http://localhost:3000/movie/"+id)
            console.warn(result)
            if(result.status==200)
            {
                this.loadData()
            }
        },
        goToUpdate(id) 
        {
            this.$router.push(`/update/${id}`);
        },
        async loadData()
        {
            let user = localStorage.getItem("user-info");
            this.name=JSON.parse(user).name;
            if(!user)
            {
                this.$router.push({name:'SignUp'})
            }
            let result=await axios.get("http://localhost:3000/movie")
            this.movie=result.data
        }
    },
    mounted()
    {
        this.loadData()
    }
}
</script>

<style>
td{
    width: 160px;
    height: 40px;
    margin-right: auto;
    margin-left: auto;
}
.table{
    margin: auto;
}
.deletebutton{
    background-color: red;
    border: 0px solid red;
    border-radius: 12%;
    cursor: pointer;
}
.update{
    background-color: green;
    border: 0px solid green;
    border-radius: 12%;
    cursor: pointer;
}
</style>