<template>
    <div>
        <v-text-field
            v-model="search"
            append-icon="mdi-magnify"
            label="Rechercher un film"
            single-line
            hide-details
        ></v-text-field>
    </div>
</template>
<script>
export default {
    name: 'MovieSearch',
    data() {
        return {
            search: ''
        }
    },
    watch: {
        search: function (val) {
            this.$emit('searchMovieEmit', val)
        }
    }
}
</script>