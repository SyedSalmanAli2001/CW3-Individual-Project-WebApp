<template>
    <div>
        <h2>Checkout</h2>
        <h3>Added subjects</h3>
        <div v-for="(subject, index) in cart" :key="index">
            <figure>
                <img width="500" height="400" v-bind:src="subject.image" />
            </figure>
            <p>Subject: {{ subject.title }}</p>
            <p>Location: {{ subject.location }}</p>
            <p>Price: {{ subject.price }}</p>
            <button @click="removeSubject(index)">remove</button>
        </div>
        <p>
            <strong> Name </strong>
            <input v-model="name" />
            <strong> Address </strong>
            <input v-model="address" />
            <button> Submit </button>
        </p>
    </div>
</template>

<script>
export default {
    name: "checkoutPage",
    props: ["cart"],
    data() {
        return {
            name: "",
            address: ""
        }
    },
    methods: {
        removeSubject(index) {
            this.$emit("removeSubject", index)
        }
    }
}
</script>