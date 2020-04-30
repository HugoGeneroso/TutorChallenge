<template>
    <div class="container">
        <div class="row tutors-title">
            <div class="h3 col col-md-12 text-center">
                Our tutors
            </div>
        </div>
        <div class="row tutors-subtitle">
            <div class="h5 col col-md-12 text-center">
               We have more than 100 tutors from various disciplines ready to match with you.
            </div>
        </div>
        <tutors-filter v-bind:sortFilter="sortFilter" v-on:inputCity="FilterCity($event)"  v-bind:cityFilter="cityFilter" v-on:inputSort="SortBy($event)"></tutors-filter>      
        <hr/>
        <div class="row" v-if="showAll">
            <div class="col col-md-3" style="margin-bottom:25px;" v-for="(tutor, index) in filteredTutors" :key="`tutor-${index}`">
                <tutor-card v-bind:tutor="tutor" v-bind:students="students[tutor.id] || []" ></tutor-card>
            </div>
        </div>
        <div class="row" v-else>
            <div class="col col-lg-3" v-for="(tutor, index) in filteredTutors.slice(0, 4)" :key="`tutor-${index}`">
                <tutor-card v-bind:tutor="tutor" v-bind:students="students[tutor.id] || []" ></tutor-card>
            </div>
        </div>
        <br />
        <div class="row">
            <div class="col col-md-12 text-center all-tutors-btn-container" v-if="showAll == false">
                <button v-on:click="EnableShowAll()" class="btn btn-light btn-lg">See all Tutors</button>
            </div>
        </div>
    </div>
</template>

<script>
    export default {  
        data(){
            return{
                tutors: [],
                filteredTutors: [],
                students: [],
                showAll: false,
                cityFilter: null,
                sortFilter: 'name',
            }
        },
        methods: {
            EnableShowAll: function (event) {
                this.showAll = true;
            },

            FilterCity: function (city) {
                var validTutors = [];
                var _this = this;
                this.tutors.forEach(tutor => {
                    if (city == tutor.city) {
                        validTutors.push(tutor);
                    }                
                });
                this.filteredTutors = validTutors;
                this.filteredTutors = validTutors.sort(function(a, b) {              
                    var textA = a[_this.sortFilter].toUpperCase();
                    var textB = b[_this.sortFilter].toUpperCase();
                    return (textA < textB) ? -1 : (textA > textB) ? 1 : 0;
                });
                this.cityFilter = city;
            },
            SortBy: function(parameter)
            {
                this.sortFilter = parameter;
                this.filteredTutors = this.filteredTutors.sort(function(a, b) {              
                    var textA = a[parameter].toUpperCase();
                    var textB = b[parameter].toUpperCase();
                    return (textA < textB) ? -1 : (textA > textB) ? 1 : 0;
                });
            }
        },
        mounted() {
            var _this = this;
            axios.get('https://my-json-server.typicode.com/HugoGeneroso/fake-rest-api/students').then(res => 
            {
                res.data.forEach(student => {                    
                    if (typeof _this.students[student.tutor] !== 'undefined') {
                        _this.students[student.tutor].push(student);
                    }else{
                        _this.students[student.tutor] = [student];
                    }
                });
                
                axios.get('https://my-json-server.typicode.com/HugoGeneroso/fake-rest-api/tutors').then(res => 
                {
                    this.tutors = res.data;
                    this.filteredTutors = res.data;
                }); 
            });
            

        }
    }
</script>
