<template>
    <div class="nav">
        <a href="/">Home</a>
        <a href="add">Add Movie</a>
        <a v-on:click="logout" href="#">Logout</a>
    </div>
</template>

<script>
export default {
    name:'Header',
    methods:{
        logout()
        {
            localStorage.clear();
            this.$router.push({name:'Login'})
        }
    }
}
</script>

<style>
.nav{
    background-color: goldenrod;
    overflow: hidden;
}
.nav a{
    float:left;
    color: aliceblue;
    padding: 14px 16px;
    text-align: center;
    font-size: 17px;
    text-decoration: none;
    margin-right: 5px;
}
.nav a:hover{
    background: #ddd;
    color: #333;
}
</style>