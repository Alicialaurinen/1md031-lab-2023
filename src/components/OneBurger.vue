<template>
  <div>
    <span id="burger">
      <h3>
        {{ burger.name }}
      </h3>
      <img class="bilder" v-bind:src="burger.img" />
      <div>
        Amount of Calories: {{ burger.kCal }}
      </div>
      <img id="spicy" v-bind:src="spicy(burger.spicy)"/>
      
      <dl id="allergi-information">
        <dt>Contains:</dt>
        <dd>{{ gluten(burger.gluten) }}</dd>
        <dd>{{ lactose(burger.lactose) }}</dd>
        <dd>{{ nuts(burger.nuts) }}</dd>
      </dl>
     
      Choose amount:
      <button v-on:click="Increase(key)"> + </button>
      {{ amountOrdered }}
      <button v-on:click="Decrease(key)"> - </button>
      <div>
        <button id="addToCart" v-on:click="addBurger()">
          <img src="img/cart.jpeg" width="30" height="30">
        </button>
      </div>
    </span>
    {{ burger.URL }}
  </div>
</template>
  
<script>
export default {
  name: 'OneBurger',
  props: {
    burger: Object
  },
  data: function () {
    return {
      amountOrdered: 0,
      
      
    }
  },
  methods: {
    Increase: function () {

      this.amountOrdered += 1;
    },
    Decrease: function () {
      if (this.amountOrdered != 0) {
        this.amountOrdered -= 1
      }
    },
    addBurger: function () {
      this.$emit('orderedBurger', {
        name: this.burger.name,
        amount: this.amountOrdered
      }
      );
    },
    lactose: function(lactose){
      if(lactose){
        return "Lactose"
      }
      else{
        return ""
      }


    },
    gluten: function(gluten){
      if(gluten){
        return "Gluten"
      }
      else{
        return ""
      }


    },
    nuts: function(nuts){
      if(nuts){
        return "Nuts"
      }
      else{
        return ""
      }
    },
    spicy: function(spicy){
      if(spicy){
        return "../img/extraspicy.png"
      }
      else{
        return "../img/spicy.png"
      }

  }
}
}
</script>
  
  <!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
/* font-family: 'Times New Roman', Times, serif; */
/*img{
    width="300" height="300"
  }*/


#allergi-information dt{
  text-decoration: underline;
  margin-left: 20px;
  
}

#allergi-information dd {
  font-weight: bold;
  
}
#addToCart{
  margin-top: 15px;
}
#spicy{
  width: 30px;
  height: 30px;
}

.bilder {
  max-width: 100%;
  max-height: 100%;

}

</style>
  