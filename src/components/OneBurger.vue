<template>
  <div>
    <span id="burger">
      <h3>
        {{ burger.name }}
      </h3>
      <img class="bilder" v-bind:src="burger.img" />
      <dl>
        <dt>Can be ordered as:</dt>
        <dd>{{ burger.gluten }}</dd>
        <dd>{{ burger.lactose }}</dd>
        <div>

        
        Amount of Calories: {{ burger.kCal }}
      </div>
      </dl>
      Choose amount:
      <button v-on:click="Increase(key)"> more </button>
      {{ amountOrdered }}
      <button v-on:click="Decrease(key)"> less </button>
      <div>
        <button v-on:click="addBurger()">
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
  