<template>
  <div id="family-page">
      <h1>Family</h1>
      <div v-if="isFull">
        <b-row>
            <b-col v-for="r in recipes" :key="r.id">
                <FamilyRecipePreview class="recipePreview" :recipe="r" />
            </b-col>
        </b-row>
      </div>
      <div v-if="isEmpty">
          There is no FAMILY Recipes 
      </div>
  </div>
</template>

<script>
import FamilyRecipePreview from "../components/FamilyRecipePreview";
export default {
    components: {
        FamilyRecipePreview,
    },
    data() {
        return {
            recipes: [],
            isFull: false,
            isEmpty: false
        }
    },
    mounted() {
        this.getFamilyRecipes();
    },
    methods: {
        async getFamilyRecipes() {
            try {
                this.axios.defaults.withCredentials = true; 
                const response = await this.axios.get(
                  "http://localhost:3000/profiles/family"
                );
                if (response.data) {
                    const recipes = response.data.data;
                    this.recipes = [];
                    this.recipes.push(...recipes);
                    this.isFull = true;
                }
                else {
                    this.isEmpty = true;
                }
            }
            catch (error) {
                console.log(error);
            }
        }
    }
}
</script>

<style>

</style>