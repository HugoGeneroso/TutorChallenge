<template>
    <div class="container">
     <div class="row">
            <div>
            <span>Filter by:</span>
            <div class="btn-group" role="group" aria-label="filter-by">
                <button type="button" v-if="cityFilter == 'Liverpool'" class="btn btn-success">Liverpool</button>
                <button type="button" v-else v-on:click="ChangeCityFilter('Liverpool')" class="btn btn-light">Liverpool</button>
                <button type="button" v-if="cityFilter == 'London'" class="btn btn-success">London</button>
                <button type="button" v-else v-on:click="ChangeCityFilter('London')" class="btn btn-light">London</button>
                <button type="button" v-if="cityFilter == 'Manchester'" class="btn btn-success">Manchester</button>
                <button type="button" v-else v-on:click="ChangeCityFilter('Manchester')" class="btn btn-light">Manchester</button>
            </div>
            </div>
            <div>
            <span class="ml-3">Sort by:</span>
            <div class="btn-group" role="group" aria-label="filter-by">
                <button type="button" v-if="sortFilter == 'name'" class="btn btn-success">Name</button>
                <button type="button" v-else v-on:click="ChangeSortFilter('name')" class="btn btn-outline-light">Name</button>
                <button type="button" v-if="sortFilter == 'city'" class="btn btn-success">City</button>
                <button type="button" v-else v-on:click="ChangeSortFilter('city')" class="btn btn-light">City</button>
            </div>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        props: ['sortFilter', 'cityFilter'],
        mounted() {
        },   
        methods: {
            ChangeSortFilter: function (sorting) {
                this.$emit('inputSort', sorting);
            },
            ChangeCityFilter: function (city) { 
                this.$emit('inputCity', city);
            }
        }
        
    }
</script>
