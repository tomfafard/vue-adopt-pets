<template>
    <div>
        <h1>{{ animal.name }} ({{$route.params.species}})</h1>
        <p>Age: {{ animal.age }} years old</p>
        <p>Breed: {{ animal.breed }}</p>
    </div>
</template>

<script>
import { mapState } from 'vuex'

export default {
    data() {
        return {
            //dogs
            animal: {}
        }
    },
    computed: {
        ...mapState([
            'cats',
            'dogs'
        ])

        // The above is equivalent to:
        //
        // cats() {
        //     return this.$store.state.cats
        // }
        // dogs() {
        //     return this.$store.state.dogs
        // }
    },
    mounted() {
       
        const animal = this[this.$route.params.species][this.$route.params.id]
        
        // Confused? the outermost "this" is being accessed via bracket notation.
        // In this case, this.$route.params.species will evaluate to either "cats" or "dogs".
        // We then reference the cats/dogs object in the mapState using: this[cats][0]

        this.animal = animal
        
    }
}
</script>