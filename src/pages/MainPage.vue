<template>
  <div class="container">
    <h1 class="title">Main Page</h1>
    <br>
    <!-- <router-link v-if="!$root.store.username" to="/login" tag="button">You need to Login to vue this</router-link>
    {{ !$root.store.username }} -->
    <h1>Random Recipes</h1>
    <div class="row">
    <div class="col-lg-4">
      <b-row id = "randoms" v-for="r in RandomRecipes" :key="r.id">
        <RecipePreview class="recipePreview" :recipe="r" />
      </b-row>
    </div>
    <div class="col-lg-4">
       <h1>Last Viewed Recipes</h1>
       <br>
      <div class = "last-viewed" v-if="lastViewdRecipes.length != 0 && this.$root.store.username">
        <b-row v-for="r in lastViewdRecipes" :key="r.id">
          <RecipePreview class="recipePreview" :recipe="r" />
        </b-row>
      </div>
      <div class = "last-viewed" v-if="lastViewdRecipes.length == 0 && this.$root.store.username">
        <h3>you didnt view any recipe yet</h3>
      </div>
      <div class = "last-viewed" v-else-if="!this.$root.store.username">
        <h4>to see last viewed recipes please log in first</h4>
        <Login/>
      </div>
    </div>
  </div>
</div>
</template>

<script>
import Login from "../pages/LoginPage";
import RecipePreview from "../components/RecipePreview";
export default {
  components: {
    RecipePreview,
    Login
  },
  data(){
    return{
      RandomRecipes:[],
      lastViewdRecipes:[]
    }
  },
  methods:{
    async getRandomRecipes(){
      let respone;
      try{
        respone = await this.axios.get("http://localhost:3000/recipes/random");
        this.RandomRecipes= [];
        this.RandomRecipes.push(...respone.data.data);
      }catch(err){
        console.log(err)
      }
    },
    async getLastViewedRecipes(){
      let respone;
      try{
        this.axios.defaults.withCredentials = true;
        respone = await this.axios.get("http://localhost:3000/profiles/last");
        if(respone.data === "No recepies viewed"){
          return;
        }else{
          this.lastViewdRecipes= [];
          this.lastViewdRecipes.push(...respone.data.data);
        }
      }catch(err){
        console.log(err)
      }
    }
  },
  mounted(){
    this.getRandomRecipes();
    if(this.$root.store.username){
      this.getLastViewedRecipes();
    }
  }
};
</script>

<style lang="scss" scoped>

// #last-viewed{
//   margin-left: 80%;
// }
// #randoms{
//   margin-right: 80%;
// }
.RandomRecipes {
  margin: 10px 0 10px;
}
.blur {
  -webkit-filter: blur(5px); /* Safari 6.0 - 9.0 */
  filter: blur(2px);
}
::v-deep .blur .recipe-preview {
  pointer-events: none;
  cursor: default;
}
</style>
