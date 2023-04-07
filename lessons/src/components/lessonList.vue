<template>
    <main>
        <div v-for="subject in subjects" :key="subject.id">
            <h2>{{ subject.title }}</h2>
            <figure>
                <img width="500" height="400" v-bind:src="subject.image" />
            </figure>
            <p>Subject: {{ subject.title }}</p>
            <p>Location: {{ subject.location }}</p>
            <p>Price: {{ subject.price }}</p>
            <p>Available stock: {{ subject.spaces }}</p>
            <button @click="addToCart(subject)">Add to cart</button>
        </div>
    </main>
</template>

<script>
export default {
    name: "LessonList",
    props:["subjects"],
    methods: {
        addToCart(subject){
            this.$emit("addSubject", subject)
        }
    }
}
</script>