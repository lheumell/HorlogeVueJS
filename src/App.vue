<template>
  <div id="app">
      <body>
        <div class="clock">
            <div class="hour" v-bind:style="{ transform: 'rotate('+ hh + ')' }"></div>
            <div class="min" v-bind:style="{ transform: 'rotate('+ mm + ')' }"></div>
            <div class="sec" v-bind:style="{ transform: 'rotate('+ ss + ')' }"></div>
        </div>
    </body>
      <h1 style="margin-top : 50px;">{{timestamp}}</h1>
      <input type="submit" value="Change" v-on:click="activePopup()" >
      <div class="popup" v-if="popupIsActive">
        <div v-if="menu === 0"><!--Menu Principal-->
        <br>
        <h1 style="text-transform: uppercase;">Change parametres</h1>
        <input type="button" value="Choisir le fuseau horaire" v-on:click="changeMenu(1)"><br>
        <input type="button" value="choisir l'heure d'une ville" v-on:click="changeMenu(2)"><br>
        <input type="button" value="modifier l'heure courante" v-on:click="changeMenu(3)"><br>
        <input type="submit" value="X" v-on:click="activePopup()">
        </div>
        
        <div v-if="menu === 1"><!--Menu 1-->
        <br>
        <h1 style="text-transform: uppercase;">Change parametres</h1>
        <input type="button" value="-9" v-on:click="changeMenu(1)"><br>
        <input type="button" value="+7" v-on:click="changeMenu(2)"><br>
        <input type="button" value="+0" v-on:click="changeMenu(3)"><br>
        <input type="button" value="-1" v-on:click="changeMenu(3)"><br>
        <input type="button" value="+8" v-on:click="changeMenu(3)"><br>
        <input type="submit" value="Valider" v-on:click="changeMenu(0) && activePopup()">
        </div>

        <div v-if="menu === 2"><!--Menu 2-->
        <br>
        <h1 style="text-transform: uppercase;">Change parametres</h1>
        <input type="button" value="Kiritimati(opposé +)" v-on:click="changeMenu(1)"><br>
        <input type="button" value="Tokyo" v-on:click="changeMenu(2)"><br>
        <input type="button" value="Paris" v-on:click="changeMenu(3)"><br>
        <input type="button" value="Los Angeles" v-on:click="changeMenu(3)"><br>
        <input type="button" value="Kamchatka(opposé -)" v-on:click="changeMenu(3)"><br>
        <input type="submit" value="Valider" v-on:click="changeMenu(0) && activePopup()">
        </div>

        <div v-if="menu === 3"><!--Menu 3-->
        <br>
        <h1 style="text-transform: uppercase;">Change parametres</h1>
        <input type="button" value="Choisir l'heure :"><br>
        <input type="button" value="Choisir les minutes :"><br>
        <input type="button" value="Choisir les secondes :"><br>
        <input type="submit" value="Valider" v-on:click="changeMenu(0) && activePopup()">
        </div>
                
        
      </div>
      <div class="masque" v-if="popupIsActive">
      </div>
  </div>
</template>

<script type="text/javascript">
//import horloge from './components/horloge.vue'

export default {
  name: 'App',
  components: {
    //horloge
  },
  data: () => ({
      timestamp: "",
      hh: "",
      mm: "",
      ss: "",
      popupIsActive: false,
      menu: 0 
  }),
  created() {
        setInterval(this.getNow, 1000);
  },
  methods: {
        getNow: function() {
            const today = new Date();
            const date = today.getFullYear()+'-'+(today.getMonth()+1)+'-'+today.getDate();
            const time = today.getHours() + ":" + today.getMinutes() + ":" + today.getSeconds();
            const dateTime = date +' '+ time;
            this.timestamp = dateTime;

            this.hh = today.getHours() * 30 + "deg" ;
            this.mm = today.getMinutes() * 6 + "deg" ;
            this.ss = today.getSeconds() * 6 + "deg" ;    
        },
        activePopup: function(){
          this.popupIsActive = !this.popupIsActive ;
        },
        changeMenu: function(nb){
          this.menu = nb ;
          console.log(this.menu);
        }
  }
}          


 
</script>


<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

    *{
    margin: 0;
    padding: 0;
    box-sizing: border-box; /*définit la façon dont la hauteur et la largeur totale d'un élément est calculée*/
    }
    body{
        display: flex;
        justify-content: center;
        align-items: center;
        /*min-height: 100vh;*/
        background-color: #091921;
    }

    .clock{
        width: 400px;
        height: 400px;
        display: flex;
        justify-content: center;
        align-items: center;
        background: url(assets/clock.png);
        background-size: cover;
        border: 4px solid #091921;
        box-shadow: 0 -15px 15px rgba(255, 255, 255, 0.05), 
        inset 0 -15px 15px rgba(255, 255, 255, 0.05), 
        0 15px 15px rgba(0, 0, 0, 0.3), 
        inset 0 15px 15px rgba(0, 0, 0, 0.3) ; /*box shadow bien integré*/
        border-radius: 50%;
    }

    .clock::before{
        content: " ";
        position: absolute;
        width: 15px;
        height: 15px;
        background-color: aliceblue;
        border-radius: 50%;
        z-index: 50;
    }


    .clock .hour{
        width: 160px;
        height: 160px;
    }

    .clock .min{
        width: 190px;
        height: 190px;
    }

    .clock .sec{
        width: 230px;
        height: 230px;
    }

    .hour, .min, .sec{
        display: flex;
        justify-content: center;
        /*align-items: center;*/
        position: absolute;
    }

    .hour::before{
        content: " ";
        position: absolute;
        width: 8px;
        height: 80px;
        background-color: crimson;
        z-index: 10 ;
        border-radius: 6px 6px 0 0;
    }

    .min::before{
        content: " ";
        position: absolute;
        width: 4px;
        height: 100px;
        background-color: whitesmoke;
        z-index: 20 ;
        border-radius: 6px 6px 0 0;
    }

    .sec::before{
        content: " ";
        position: absolute;
        width: 2px;
        height: 150px;
        background-color: whitesmoke;
        z-index: 30 ;
        border-radius: 6px 6px 0 0;
    }

    input{
      border: 1px solid white;
      border-radius: 5%;
      padding: 10px 15px 10px 15px;
      color: white;
      background-color: transparent;
      margin-top: 50px ;
      transition: all 0.5s;
    }

    input:hover{
      background-color: white;
      color: #091921;
    }

    .popup{
      position: absolute;
      width: 800px;
      height: 500px;
      box-shadow: 0 0 15px white;
      background-color: #091921;
      position: absolute; /* postulat de départ */
      top: 50%; left: 50%; /* à 50%/50% du parent référent */
      transform: translate(-50%, -50%); /* décalage de 50% de sa propre taille */
      z-index: 1000;
    }

    .masque{
      position: absolute;
      z-index: 500;
      top: 0; left: 0;
      height: 100%;
      width: 100%;
      background-color: gray;
      opacity: 25%;
    }
</style>

