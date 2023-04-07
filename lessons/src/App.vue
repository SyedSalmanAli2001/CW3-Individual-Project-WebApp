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
      subjects: [
        {
          id: 1001,
          title: "Mathematics",
          location: "Dubai",
          price: '40',
          image: 'mathematics.jpeg',
          spaces: 5,

        },
        {
          id: 1002,
          title: "History",
          location: "Dubai",
          price: '50',
          image: 'history.jpeg',
          spaces: 5,

        },
        {
          id: 1003,
          title: "Physics",
          location: "Sharjah",
          price: '30',
          image: 'physics.jpeg',
          spaces: 5,

        },
        {
          id: 1004,
          title: "Information Technology",
          location: "Ras Al-Khaima",
          price: '55',
          image: 'it.jpeg',
          spaces: 5,

        },
        {
          id: 1005,
          title: "Biology",
          location: "Dubai",
          price: '45',
          image: 'biology.jpeg',
          spaces: 5,

        },
        {
          id: 1006,
          title: "Chemistry",
          location: "Al Ain",
          price: '35',
          image: 'chemistry.jpeg',
          spaces: 5,

        },
        {
          id: 1007,
          title: "English Language",
          location: "Dubai",
          price: '60',
          image: 'english.jpeg',
          spaces: 5,

        },
        {
          id: 1008,
          title: "Geography",
          location: "Abu Dhabi",
          price: '25',
          image: 'geography.jpeg',
          spaces: 5,

        },
        {
          id: 1009,
          title: "Drama",
          location: "Sharjah",
          price: '40',
          image: 'drama.jpeg',
          spaces: 5,

        },
        {
          id: 1010,
          title: "Art",
          location: "Dubai",
          price: '35',
          image: 'art.webp',
          spaces: 5,

        }
      ]
    }
  },
  computed: {
    currentComponent: function () {
      return this.showCheckout ? "checkout" : "lessonList";
    },
  },
  methods: {
    switchCheckout: function () {
      this.showCheckout = !this.showCheckout;
    },
    addToCart(subject) {
      const index = this.subjects.findIndex((sub) => sub.id === subject.id);
      if (index >= 0 && this.subjects[index].spaces > 0) {
        this.subjects[index].spaces--;
        this.cart.push(subject);
      }
    },
    removeFromCart(index) {
      const subject = this.cart[index];
      this.cart.splice(index, 1);
      this.returnSubject(subject);
    },
    returnSubject(subject) {
      const index = this.subjects.findIndex((sub) => sub.id === subject.id);
      if (index >= 0) {
        this.subjects[index].spaces++;
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
