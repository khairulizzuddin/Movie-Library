<template>
    <Header />
    <h1>Add</h1>
    <form class="add">
        <input type="text" name="name" placeholder="Enter Name" v-model="movie.name" />
        <input type="text" name="release" placeholder="Enter Year Release" v-model="movie.release" />
        <input type="text" name="rating" placeholder="Enter Rating" v-model="movie.rating" />
        <button type="button" v-on:click="addMovie">Add New Movie</button>
    </form>
</template>

<script>
import Header from './Header.vue'
import axios from 'axios'
export default{
    name:'Add',
    components:{
        Header
    },
    data()
    {
        return{
            movie:{
                name:'',
                release:'',
                rating:''
            }
        }
    },
    methods:{
        async addMovie()
        {
            console.warn(this.movie)
            const result= await axios.post("http://localhost:3000/movie",{
                name:this.movie.name,
                release:this.movie.release,
                rating:this.movie.rating
            });
            if(result.status==201)
            {
                this.$router.push({name:'Home'})
            }
        }
    },
    mounted()
    {
        let user = localStorage.getItem("user-info");
        if(!user)
        {
            this.$router.push({name:'SignUp'})
        }
    }
}
</script>