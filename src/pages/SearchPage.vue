<template>
  <div class="container">
      <h1>Search Page</h1>
      <div>
        <b-form @submit.prevent="handleSearch" >
        <p>search for recipes:</p>
        <div class="active-cyan-3 active-cyan-4 mb-4" id = "query">
        <input class="form-control" v-model="searchForm.query" type="text" placeholder="name of recipe or dish" aria-label="Search">
        </div>  
        <b-form-group class = form
          id="group-for-cusine"
          description=""
          label="Cusine"
          label-for="cusines"
        >
        <b-form-select id="cusines" v-model="searchForm.cusine" :options="cusines"></b-form-select>
        </b-form-group>
        <b-form-group class = form
          id="group-for-diet"
          description=""
          label="Diet"
          label-for="diets"
        >
        <b-form-select id="diets" v-model="searchForm.diet" :options="diets"></b-form-select>
        </b-form-group>
        <b-form-group class = form
          id="group-for-intolerance"
          description=""
          label="Intolerance"
          label-for="intolerance"
        >
        <b-form-select id="intolerance" v-model="searchForm.intolorence" :options="intolerances"></b-form-select>
        </b-form-group>
        <b-form-group
          id="group-for-amount"
          description=""
          label="Number Of Results"
          label-for="amount"
        >
        <b-form-select id="amount" v-model="searchForm.amount" :options="amounts"></b-form-select>
        </b-form-group>
        <input class="btn btn-primary" type="submit" value="Search">   <input class="btn btn-primary" type="reset" value="Reset">
        </b-form>
      </div>
      <br>
     <b-dropdown id="sort" text="sort by" class="m-md-2">
        <b-dropdown-item @click= "sortByPopularity">Popularity</b-dropdown-item>
        <b-dropdown-item @click= "sortByPreperationTime">Preperation Time</b-dropdown-item>
      </b-dropdown>  
    <div v-if="this.recipes.length != 0">
      <RecipePreview
        v-for="r in recipes"
        :key="r.id"
        :recipe = "r"
      />
    </div>
    <div v-else-if="this.recipes.length == 0">
      <RecipePreview
        v-for="r in lastSearchResults"
        :key="r.id"
        :recipe = "r"
      />
    </div>
  </div>
</template>

<script>
  import cusineArr from "../assets/cusine";
  import dietArr from "../assets/diet";
  import intoleranceArr from "../assets/intolorences.js";
  import RecipePreview from "../components/RecipePreview";
export default {
  components: {
    RecipePreview,
  },
  data() {
      return {
        recipes:[],
        lastSearchResults:[],
        searchForm:{
          query:null,
          amount:null,
          cusine:null,
          intolorence:null,
          diet:null
        },
        cusines: [{ value: null, text: "", disabled: true }],
        diets: [{ value: null, text: "", disabled: true }],
        intolerances: [{ value: null, text: "", disabled: true }],
        amounts: [{ value: null, text: "", disabled: true }],
     }
  },
  mounted(){
      this.cusines.push("");
      this.cusines.push(...cusineArr);
      this.diets.push("");
      this.diets.push(...dietArr);
      this.intolerances.push("");
      this.intolerances.push(...intoleranceArr);
      this.amounts.push(5);
      this.amounts.push(10);
      this.amounts.push(15);
      this.searchForm.amount = 5;
       if (this.$root.store.username){
        if (localStorage.getItem("lastSearchFormByUser") != undefined) {
        this.searchForm = JSON.parse(localStorage.getItem("lastSearchFormByUser"));
        } 
        this.lastSearchResults = JSON.parse(localStorage.getItem("lastSearchByUser"));
      }
  },
  methods:{
    async handleSearch(){ 
      let respone;
      try{
        respone = await this.axios.get("http://localhost:3000/recipes/search/query/" 
        + this.searchForm.query + "/number/" 
        + this.searchForm.amount,
        {
          params:{
            cuisine: this.searchForm.cusine,
            diet: this.searchForm.diet,
            intolerances: this.searchForm.intolorence
          }
        });
        this.recipes = [];
        this.lastSearchResults = [];
        this.recipes.push(...respone.data.data);
        if(this.recipes.length == 0){
          alert("No Recipes Found")
        }
        if (this.$root.store.username) {
          this.$root.store.saveLastSearchFormByUser(this.searchForm);
          this.$root.store.saveLastSearchByUser(this.recipes);
          this.lastSearchResults = JSON.parse(localStorage.getItem("lastSearchByUser"));
        }
      }catch(err){
        console.log(err);
      }
    },
    handleReset(){
      this.searchForm.query = null;
      this.searchForm.diet = null;
      this.searchForm.intolorence = null;
      this.searchForm.cusine = null;
      this.searchForm.amount = 5;
    },
    sortByPopularity(){
      if(this.recipes && this.recipes.length !=0){
        this.recipes.sort(function(a,b){
          return a.aggregateLikes - b.aggregateLikes
        });
      }else if(this.lastSearchResults && this.lastSearchResults.length != 0){
        this.lastSearchResults.sort(function(a,b){
          return a.aggregateLikes - b.aggregateLikes
        });
      }
    },
    sortByPreperationTime(){
       if(this.recipes && this.recipes.length !=0){
        this.recipes.sort(function(a,b){
          return a.readyInMinutes - b.readyInMinutes
        });
       }else if(this.lastSearchResults && this.lastSearchResults.length != 0){
        this.lastSearchResults.sort(function(a,b){
          return a.readyInMinutes - b.readyInMinutes
        });
      }
    }

  }
}
</script>

<style>
  .form{
    float: left;
    margin-right: 15%;
  }

  #query{
     margin-right: 15%;
  }

  #group-for-amount{
    margin-right: 85%;
  }
</style>