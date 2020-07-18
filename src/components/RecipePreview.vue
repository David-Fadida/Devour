<template>
  <router-link
    :to="{ name: 'aboute' }"
    class="recipe-preview"
    @mouseover="hover = true"
    @mouseleave="hover = false"
  >
    <div class="recipe-body">
      <img v-if="image_load" :src="recipe.image" class="recipe-image" />
    </div>
    <div class="recipe-footer">
      <div :title="recipe.title" class="recipe-title">
        {{ recipe.title }}
      </div>
      <ul class="recipe-overview">
        <li>
          <font-awesome-icon id="prepDuration" :icon="['far', 'clock']" size="lg"/>
          {{ recipe.readyInMinutes }} mins
        </li>
        <li>
          <font-awesome-icon id="likes" icon="heart" size="lg"/>
          {{ recipe.aggregateLikes }} likes
        </li>
      </ul>
      <div class="recipe-info">
        <!-- VEGAN -->
        <font-awesome-icon v-if="recipe.vegetarian" icon="leaf" size="2x"/>
        <!-- VEGETATRIAN -->
        <font-awesome-icon v-else-if="recipe.vegan" icon="seedling" size="2x"/>
        <!-- GLUTEN FREE -->
        <font-awesome-icon v-if="recipe.glutenFree" icon="ribbon" size="2x"/>
        <!-- VISITED -->
        <font-awesome-icon v-if="recipe.visited" icon="eye" size="2x"/>
        <!-- FAVORITE -->
        <font-awesome-icon v-if="!recipe.favorite" :icon="['far', 'star']" size="2x"/>
        <font-awesome-icon v-else-if="recipe.favorite" :icon="['fas', 'star']" size="2x"/>
      </div>
    </div>
  </router-link>
</template>

<script>
export default {
  mounted() {
    this.axios.get(this.recipe.image).then((i) => {
      this.image_load = true;
    });
  },
  data() {
    return {
      image_load: false,
      hover: false
    };
  },
  props: {
    recipe: {
      type: Object,
      required: true
    }
  },
  
};
</script>

<style scoped>
.recipe-preview {
  font-family: 'Palanquin Dark';
  display: inline-block;
  width: 90%;
  height: 100%;
  position: relative;
  margin: 10px 10px;
  -webkit-box-shadow: 6px 6px 10px -1px rgba(0,0,0,0.56);
  -moz-box-shadow: 6px 6px 10px -1px rgba(0,0,0,0.56);
  box-shadow: 6px 6px 10px -1px rgba(0,0,0,0.56);
  cursor: pointer;
  border: rgb(122, 122, 122) solid 1px;
}
.recipe-preview:hover {
  transition-duration: 0.5s;
  transform: scale(1.05);
}
.recipe-preview > .recipe-body {
  width: 100%;
  height: 200px;
  position: relative;
}
.recipe-preview .recipe-body .recipe-image {
  margin-left: auto;
  margin-right: auto;
  margin-top: auto;
  margin-bottom: auto;
  display: block;
  width: 100%;
  height: 100%;
  -webkit-background-size: cover;
  -moz-background-size: cover;
  background-size: cover; 
  
}
.recipe-preview .recipe-footer {
  width: 100%;
  height: 50%;
  overflow: hidden;
}
.recipe-preview .recipe-footer .recipe-title {
  padding: 10px 10px;
  width: 100%;
  font-size: 16pt;
  text-align: center;
  white-space: nowrap;
  overflow: hidden;
  -o-text-overflow: ellipsis;
  text-overflow: ellipsis;
  color: black;
  margin-bottom: 1%;
}
.recipe-preview .recipe-footer ul.recipe-overview {
  padding: 5px 10px;
  width: 100%;
  display: -webkit-box;
  display: -moz-box;
  display: -webkit-flex;
  display: -ms-flexbox;
  display: flex;
  -webkit-box-flex: 1;
  -moz-box-flex: 1;
  -o-box-flex: 1;
  box-flex: 1;
  -webkit-flex: 1 auto;
  -ms-flex: 1 auto;
  flex: 1 auto;
  table-layout: fixed;
  margin-bottom: 0px;
}
.recipe-preview .recipe-footer ul.recipe-overview li {
  -webkit-box-flex: 1;
  -moz-box-flex: 1;
  -o-box-flex: 1;
  -ms-box-flex: 1;
  box-flex: 1;
  -webkit-flex-grow: 1;
  flex-grow: 1;
  width: 90px;
  display: table-cell;
  text-align: center;
  color: black;
}
.recipe-info{
  text-align: center;
  margin-top: 5%;
  margin-bottom: -3%;
  padding-left: 5%;
  padding-right: 5%;
  font-size: 80%;
  color: black;
}
a:hover { 
  text-decoration: none; 
}
#likes,
#prepDuration{
  margin-right: 5px;
  margin-left: 5px;
}
</style>