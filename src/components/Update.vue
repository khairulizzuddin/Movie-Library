<template>
    <Header />
    <h1>Update</h1>
    <form class="add">
        <input type="text" name="name" placeholder="Enter Name" v-model="movie.name" />
        <input type="text" name="release" placeholder="Enter Year Release" v-model="movie.release" />
        <input type="text" name="rating" placeholder="Enter Rating" v-model="movie.rating" />
        <button type="button" v-on:click="updateMovie">Update Movie</button>
    </form>
</template>

<script>
import Header from './Header.vue'
import axios from 'axios'
export default{
    name:'Upate',
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
        async updateMovie()
        {
            console.warn(this.movie)
            const result= await axios.put("http://localhost:3000/movie/"+this.$route.params.id,{
                name:this.movie.name,
                release:this.movie.release,
                rating:this.movie.rating
            });
            if(result.status==200)
            {
                this.$router.push({name:'Home'})
            }
        }
    },
    async mounted()
    {
        let user = localStorage.getItem("user-info");
        if(!user)
        {
            this.$router.push({name:'SignUp'})
        }
        const result = await axios.get("http://localhost:3000/movie/"+this.$route.params.id)
        console.warn(this.$route.params.id)
        console.warn(result.data)
        this.movie=result.data
    }
}
</script>