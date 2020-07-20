<template>
  <div class="container">
    <h1 class="title">Main Page</h1>
    <br>
    <!-- <router-link v-if="!$root.store.username" to="/login" tag="button">You need to Login to vue this</router-link>
    {{ !$root.store.username }} -->
    <h1>Random Recipes</h1>
    <div class="row">
    <div class="col-lg-4">
      <input class="btn btn-primary" type="submit" value="New Random Recipes" @click="getRandomRecipes">
      <b-row id = "randoms" v-for="r in RandomRecipes" :key="r.id">
        <RecipePreview class="recipePreview" :recipe="r" />
      </b-row>
    </div>
    <div class="col-lg-4">
      <div>
        <lastReciepesSeen v-if="this.$root.store.username"/>
      </div>
      <div class = "last-viewed" v-if="!this.$root.store.username">
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
import lastReciepesSeen from "../components/lastReciepesSeen";
export default {
  components: {
    RecipePreview,
    Login,
    lastReciepesSeen
  },
  data(){
    return{
      RandomRecipes:[],
      isEmpty:false,
      isFull:false
    }
  },
  methods:{
    async getRandomRecipes(){
      console.log("EEEEitan")
      let respone;
      try{
        respone = await this.axios.get("http://localhost:3000/recipes/random");
        this.RandomRecipes= [];
        this.RandomRecipes.push(...respone.data.data);
      }catch(err){
        console.log(err)
      }
    },
  },
  mounted(){
    this.getRandomRecipes();
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
