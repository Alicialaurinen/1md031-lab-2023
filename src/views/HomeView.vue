<template>
   
  <header>
        <h1>Burgers Online</h1>

    </header>
    <main>
        <section class="Burgers" id="chooseburger">
            <h2> Select burger </h2>
            <p1> This is where you select burger </p1>
            <div class="wrapper">
              <Burger v-for="burger in burgers"
              v-bind:burger="burger" 
              v-bind:key="burger.name"
              v-on:orderedBurger="addToOrder($event)"/>
            </div>

        </section>

        <section id="contact">
            <h4>
                Enter customer information
            </h4>
            <form>
              
                <p>
                    <label for="firstname">Full name</label><br>
                    <input type="text" id="firstname" v-model="fn" required="required" placeholder="First and lastname">
                  
                </p>
                <p>
                    <label for="email">E-mail</label><br>
                    <input type="email" id="email" v-model="em" required="required" placeholder="E-mail address">
                </p>
                <p>
                    <label for="street">Street</label><br>
                    <input type="text" id="street" v-model="st" required="required" placeholder="Street name">

                </p>
                <p>
                    <label for="housenumber">Street</label><br>
                    <input type="number" id="housenumber" v-model="hn" required="required" placeholder="House number"
                        maxlength="10">
                </p>

                <section id = "map-container">
                  
                  <div id="map" v-on:click="addOrder" >
                      click here
                  
                 <div id = "dots" v-bind:style="{left: location.x + 'px', top: location.y + 'px'}" v-bind:key="'dots' + key" v-on:click="setLocation">
                  {{key}}
                 </div>
                </div>
                  
                  </section>
                <p>
                    <label for="payment">Payment method</label><br>
                    <select id="paymentmethod" v-model="pm">
                        <option>Klarna</option>
                        <option selected="selected">Swish</option>
                        <option>Debit-Card</option>
                        <option>Credit-Card</option>
                        <option>Svea</option>

                    </select>
                </p>
                <p style="display: inline-block">
                    <label for="gender">Gender</label><br>
                    <label>
                        <input type="radio" v-model="gender" value="Female" checked> Female
                    </label>
                    <label>
                        <input type="radio" v-model="gender" value="Male"> Male
                    </label>
                    <label>
                        <input type="radio" v-model="gender" value="unspecified"> Do not wish to provide
                    </label>
                </p>

              </form>
            
            
            <button  class= "button"  type="submit" v-on:click="markDone"> Place Order
                <img src="img/send.png" width="70" height="30">
            </button> <br>
            

        </section>



    </main>
    <footer>
        <hr>
        &COPY; 2023 ALLES BURGERS INC.

    </footer>
</template>

<script>
import Burger from '../components/OneBurger.vue'
import io from 'socket.io-client'
import menu from '../assets/menu.json'

const socket = io();

// function menuItem(nm , kc, url, gl, lac){
//   this.name = nm;
//   this.kcal = kc;
//   this.gluten = gl;
//   this.lactose = lac;
//   this.URL = url;
  
// }
// let allBurgers = [{name: "The Mouth-Watering Burger", kCal: 900, url:"img/Mouthwateringburger.jpeg ", gluten: "Gluten-Free", lactose: "Lactose-Free"},
// {name: "The Devils-Burger", kCal: 100, url:"img/devils burger - stor – medel.jpeg", gluten: "Gluten-free", lactose: "Vegan" },
// {name: "The Basic Cheese-Burger", kCal: 500, url:"img/THEcheeseburger.jpeg", gluten:"Fat-Free" , lactose: "Lactose-Free"}]
// console.log(allBurgers)


export default {
  name: 'HomeView',
  components: {
    Burger
  },
  data: function () {
    return {
      burgers: menu,
      fn: '',
      em:'',
      st:'',
      hn:'',
      pm:'',
      gender:'',
      orderedBurgers: {},
      location: { x: 0, y: 0}
    }
  },
    
  
  methods: {
    getOrderNumber: function () {
      return Math.floor(Math.random()*100000);
    },
    addOrder: function (event) {
      var offset = {x: event.currentTarget.getBoundingClientRect().left,
                    y: event.currentTarget.getBoundingClientRect().top};
      socket.emit("addOrder", { orderId: this.getOrderNumber(),
                                details: { x: event.clientX - 10 - offset.x,
                                           y: event.clientY - 10 - offset.y },
                                orderItems: ["Beans", "Curry"]
                              }
                 );
    },
    addToOrder: function (event) {
      this.orderedBurgers[event.name] = event.amount;

    console.log(this.orderedBurgers)

  
},
    markDone: function (){
        // socket.emit("addClient", { contact: this.contact,
        //                         firstName: this.fn,
                                
        //                       }
        //          );
       // console.log(this.fn, this.em, this.st, this.hn, this.pm, this.gender)
        
      
       },
       setLocation: function(event){
        this.location.x= event.clientX - 10 - event.currentTarget.getBoundingClientRect().left;
        this.location.y= event.clientY - 10 - event.currentTarget.getBoundingClientRect().top;
        console.log(this.location)
       },

    }
  }

</script>

<style>
 #map-container{
    overflow: scroll;
    height: 200px;
  }
  #map {
    background: url("../../public/img/polacks.jpg");
    background-size: cover;
    width: 100%;
    height: 100vh;
  }
 

body {
    font-family: 'Times New Roman', Times, serif;
 }
 header {
    background-image: url("../../public/img/bakgrundhamburger.jpeg");
    opacity: 0.8;
    text-align: center;
    height: 410px;
    color: black;
    overflow:hidden;
    width: 100%;

 }
 
 h3{
    padding: 20px;
    font-size: 20px
 }

 .Burgers {
    margin-top: 20px;
    margin-left: 20px;
    margin-right: 20px;
    margin-bottom: 20px;
    border: 15px double whitesmoke;
    text-align: center;
    
    
 }

 #chooseburger { 
    background-color: black;
    color: whitesmoke;

 }

 div {

    /* padding: 10px 65px 10px; */
    margin: 1px 2px 3px 4px;

 }

 button:hover {
    background-color: blueviolet;
    cursor: pointer;
 }

 #contact {
    border: 5px dashed darkgreen;
    background-color: aquamarine;
    margin-left: 20px;
    margin-right: 20px;

 }
 
 .wrapper {
  margin-top: 70px;
  margin-bottom: 30px;
    display: grid;
    width:100%;
    grid-column-gap: 1px;
    grid-template-columns: repeat(3,1fr);
}
.bilder {
  width: 300px;
  height: 200px;

} 
.button {
    margin-top: 50px;
    margin-bottom: 10px;
    width: 70; 
    height: 30;

 }
 #dots {
    position: relative;
    margin: 0;
    padding: 0;
    background-repeat: no-repeat;
    width:1920px;
    height: 1078px;
    cursor: crosshair;
  }
  #dots div {
    position: absolute;
    background: black;
    color: white;
    border-radius: 10px;
    width:20px;
    height:20px;
    text-align: center;
  }


</style>