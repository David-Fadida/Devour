<template>
   <div>
    <h1>Favorites Recipes</h1>
    <RecipePreview
      v-for="r in recipes"
      :recipe="r"
      :key="r.id"
    />
   </div>
</template>

<script>
import RecipePreview from "../components/RecipePreview";
export default {
    components: {
        RecipePreview
    },
    data(){
        return{
            recipes:[]
        };
    },
    methods:{
        async getFaves(){
            this.recipes = [];
            let respone;
            this.axios.defaults.withCredentials = true;
            try{
                respone = this.axios.get("http://localhost:3000/profile/favorites");
                this.recipes.push(...respone.data.data);
            }catch(err){
                console.log(err);
                 this.$router.replace("/NotFound");
            }
        }
    },
    mounted(){
        this.getFaves();
    }
}
</script>

<style>

</style>