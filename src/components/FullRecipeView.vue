<template>
  
</template>

<script>
export default {
    methods:{
        async addToFavorites(){
            try{
            this.axios.defaults.withCredentials = true;
            await this.axios.post(
                "http://localhost:3000/profile/favorites",{
                 recipe:this.recipe.id,
                }
            );
            }catch(err){
                console.log(err)
            }
        }
    }
}
</script>

<style>

</style>