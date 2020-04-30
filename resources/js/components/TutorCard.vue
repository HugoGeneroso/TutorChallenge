<template>
    <div class="container">
        <div class="card">
            <img class="card-img-top"  style="height:100%;" src="images/user-photo.jpg" alt="User photo">
            <div class="card-body bg-light">
                <h5 class="card-title">{{tutor.name}}</h5>
                <span class="card-span">City</span>
                <br />
                <p class="badge badge-light bg-white">{{tutor.city}}</p>
                <br />                    
                <span class="card-span">Students so far</span>
                <div class="row" style="min-height:35px">
                    <div class="col col-md-2" v-for="(student, index) in students.slice(0,4)" :key="`tutor-${index}`">
                        <img class="card-img-top rounded-circle" :title="student.name" style="width: 32px;height:32px; margin-left:5px;" src="images/student-photo.jpg">
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        props: ['tutor', 'students'],
        mounted() {
        }
    }
</script>
