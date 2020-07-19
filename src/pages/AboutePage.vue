<template>
<div>
  <div class="about-section">
  <h1>About Us</h1>
  <p>We are 2 students from BGU university, finishing our third year for Software and Information Systems Engineering.
     </p>
    
  
 </div>

<h2 style="text-align:center">Our Team</h2>
<div id="Eitan" class="row" style="margin-left:23%">
  <div class="column">
    <div class="card">
      <img id="dekel" src="../assets/Eitan.jpg" alt="Jane" style="width:100%">
      <div class="container">
        <h2>Eitan Platok</h2>
        <p class="title">student</p>
        <p>3rd year student for Software and Information Systems Engineering. lives in beer sheva.</p>
        <p>eitanpl@post.bgu.ac.il</p>
        <p><button class="button">Contact</button></p>
      </div>
    </div>
  </div>

 
  
  <div class="column">
    <div class="card">
      <img src="../assets/Eitan.jpg" alt="John" style="width:100%">
      <div class="container">
        <h2>David Fadida</h2>
        <p class="title">student</p>
        <p>3rd year student for Software and Information Systems Engineering. lives in ashkelon.</p>
        <p>davidfad@post.bgu.ac.il</p>
        <p><button class="button">Contact</button></p>
      </div>
    </div>
  </div>
</div>
<br>
<div id="extraProjects" style = "text-align:center">
  <h4>for more of our projects:</h4>
    <h5><a href="https://sise-web-development-environments.github.io/assignment2-eitan-and-david">Pacman</a></h5>
   <h5><a href="https://sise-web-development-environments.github.io/313125353/">Eitan's Land Page</a></h5>
   <h5><a href="https://sise-web-development-environments.github.io/assignment1-David-Fadida/">David's Land Page</a></h5>
</div>
</div>


</template>

<script>
export default {

}
</script>

<style>
/* body {
  font-family: Arial, Helvetica, sans-serif;
  margin: 0;
}

html {
  box-sizing: border-box;
}

*, *:before, *:after {
  box-sizing: inherit;
}

.column {
  float: left;
  width: 33.3%;
  margin-bottom: 16px;
  padding: 0 8px;
}

.card {
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2);
  margin: 8px;
}

.about-section {
  padding: 50px;
  text-align: center;
  background-color: #474e5d;
  color: white;
}

.container {
  padding: 0 16px;
}

.container::after, .row::after {
  content: "";
  clear: both;
  display: table;
}

.title {
  color: grey;
}

.button {
  border: none;
  outline: 0;
  display: inline-block;
  padding: 8px;
  color: white;
  background-color: #000;
  text-align: center;
  cursor: pointer;
  width: 100%;
}

.button:hover {
  background-color: #555;
}

@media screen and (max-width: 650px) {
  .column {
    width: 100%;
    display: block;
  }

#extraProjects{
  text-align: center;
}  


} */
</style>