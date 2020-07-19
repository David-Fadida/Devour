<template>
    <div>
    <div id = "personal" class="row">
    <div v-if="hasPersonalRecipes" class="col-lg-4">
      <h1>Personal Recipes</h1>
      <b-row  v-for="r in recipes" :key="r.id">
        <RecipePreview class="recipePreview" :recipe="r" :personalRecipeId="r.title" />
      </b-row>
    </div>
    <div v-else-if="dontHave">
        <h1>you dont have personal recipes</h1>
    </div>
    </div>
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
            recipes:[],
            hasPersonalRecipes:false,
            dontHave:false
        };
    },
    methods:{
        async getPersonalRecipes(){
            this.recipes = [];
            let respone;
            this.axios.defaults.withCredentials = true;
            try{
                respone = await this.axios.get("http://localhost:3000/profiles/private");
                console.log(respone)
                if(respone.data){
                    this.recipes.push(...respone.data.data);
                    this.hasPersonalRecipes = true;
                }else{
                    this.dontHave = true;
                }
                
            }catch(err){
                console.log(err);
                 this.$router.replace("/NotFound");
            }
        }
    },
    mounted(){
        this.getPersonalRecipes();
    }
}
</script>

<style>
#personal{
margin-left: 38%;
}
</style>