<template>
  <div id="app">
    <header>
      <h1>{{ sitename }}</h1>
      <button @click="switchCheckout">{{ this.cart.length }} {{ showCheckout ? 'Back' : 'Checkout' }} </button>
    </header>
    <main>
      <component v-bind:is="currentComponent" :cart="cart" @removeSubject="removeFromCart" :subjects="subjects"
        @addSubject="addToCart"></component>
    </main>
  </div>
</template>

<script>
import lessonList from './components/lessonList.vue'
import checkout from './components/checkout.vue'

export default {
  name: 'App',
  components: {
    lessonList,
    checkout
  },
  data() {
    return {
      sitename: "After School Lessons",
      cart: [],
      showCheckout: false,
      subjects: []
    }
  },
  computed: {
    currentComponent: function () {
      return this.showCheckout ? "checkout" : "lessonList";
    },
  },
  created: function () {
    const subject = this;
    fetch("http://localhost:3000/collection/lessons").then(function (response) {
      response.json().then(function (json) {
        subject.subjects = json;
      });
    });
  },
  methods: {
    switchCheckout: function () {
      this.showCheckout = !this.showCheckout;
    },
    addToCart(subject) {
      const index = this.subjects.findIndex((sub) => sub._id === subject._id);
      if (index >= 0 && this.subjects[index].space > 0) {
        this.subjects[index].space--;
        this.cart.push(subject);
      }
    },
    removeFromCart(index) {
      const subject = this.cart[index];
      this.cart.splice(index, 1);
      this.returnSubject(subject);
    },
    returnSubject(subject) {
      const index = this.subjects.findIndex((sub) => sub._id === subject._id);
      if (index >= 0) {
        this.subjects[index].space++;
      }
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
</style>
