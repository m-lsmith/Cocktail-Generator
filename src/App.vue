<template>
  <div class="gradient" id="container">
    <div id="leftSide">
        <h1> Cocktail Generator </h1>
        <button @click="fetchData" id="getActivity"></button>
        <h4 id="activity">Get A Random Cocktail!</h4>
        <h4 id="name"> {{drinksInfo.strDrink}}</h4>
        <p id="isAlcoholic"> </p>
        <p id="mainIngredient"> </p>
        <p id="glass"></p>
    </div>

    <div id="rightSide">
            <div id="drinkImageCont">
              <img id="drinkImage" :src= drinksInfo.strDrinkThumb>
            </div>
            
    </div>
  </div>     
</template> 

<script>


export default {
  name: 'App',
  components: {
   
  },
  data () {
    return {
      info: null,
      drinksInfo: "",
      ingredients: [],
      drinkimg: "https://via.placeholder.com/300"
    }
  },
 methods: {
   fetchData() {
    fetch("https://www.thecocktaildb.com/api/json/v1/1/random.php")
    .then(response => response.json())
    .then(data => {
      data = data.drinks[0]
      this.drinksInfo = data
      console.log("drinksInfo:", this.drinksInfo)
      document.getElementById("activity").innerHTML = "";
      this.drinkimg = this.drinksInfo.strDrinkThumb
      document.getElementById("mainIngredient").innerHTML = `Main Ingredient: ${this.drinksInfo.strIngredient1}`
      document.getElementById("glass").innerHTML = `Serving Glass: ${this.drinksInfo.strGlass}`
      this.alcoholicCheck()
    
    
    }
      )
    

    
  },
  alcoholicCheck() {
    if (this.drinksInfo.strAlcoholic)
    {
      document.getElementById("isAlcoholic").innerHTML = "Alcoholic: Yes";
    }
    else {
      document.getElementById("isAlcoholic").innerHTML = "Alcoholic: No";
    }
    
  
  }
    }  
 }

</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Roboto+Mono:wght@200&display=swap');

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
 
#getActivity {
  height: 100px;
  width: 100px;
  border-radius: 50%;
  background-color: #FFBEEF;
  border: 1px solid #FFBEEF;
  cursor: pointer;
  transition: all 0.2s;
  box-shadow:  0 2px 4px #4B3B47;
}

#getActivity:hover{
 background-color: rgba(240, 46, 170, 0.4);
 border: 1px solid rgba(220, 43, 155, 0.4);
 box-shadow: rgba(0, 0, 0, .3) 2px 8px 8px -5px;
  transform: translate3d(0, 2px, 0);
}


body {
  background-image: url(/assets/sky.png);
}

#drinkImage {
  width: 75%;
  height: auto;
}

#container {
  display: flex;
  justify-content: space-between;
  align-items: center;
  background-color: hwb(240 87% 0%);
  width: 50%;
  height: 500px;
  border: rgba(240, 46, 170, 0.4) 2px solid;
  box-shadow: rgba(240, 46, 170, 0.4) 5px 5px, rgba(240, 46, 170, 0.3) 10px 10px, rgba(240, 46, 170, 0.2) 15px 15px, rgba(240, 46, 170, 0.1) 20px 20px, rgba(240, 46, 170, 0.05) 25px 25px;
  margin: auto;
  font-family: 'Roboto Mono', monospace;
}

#leftSide {
  padding-left: 20px;
  width: 20%;
}


</style>
