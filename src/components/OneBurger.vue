<template>
    <div>
      <span id="burger">
                        <h3>
                          {{ burger.name }}
                        </h3>
                        <img class="bilder" v-bind:src="burger.img"/>
                        <dl>
                            <dt>Can be ordered as:</dt>
                            <dd>{{ burger.gluten }}</dd>
                            <dd>{{burger.lactose}}</dd>
                            <dd>Calories: {{ burger.kCal }}</dd>
                        </dl>
                       <button v-on:click="Increase()"> more </button> {{amountOrdered}} <button v-on:click="Decrease()"> less </button>
                    </span>
       {{ burger.URL}}
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
  Increase: function() {
    this.amountOrdered += 1;
    this.$emit('orderedBurger', { name:   this.burger.name, 
                                amount: this.amountOrdered 
                              }
  );
  console.log("hello")
  },
  Decrease: function(){
    this.amountOrdered -= 1
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
  .bilder {
    max-width: 100%;
  }
  </style>
  