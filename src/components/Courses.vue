<template>
    <div id="courses-container" :class="{'tab active' : coursesSelected, 'tab' : !coursesSelected}">
        <h1 class="title">Courses</h1>
        <table id="courses">
            <thead>
            <tr>
                <th>#</th>
                <th>Course Title</th>
                <th>Semester</th>
                <th>Grade</th>
            </tr>
            </thead>
            <tbody>
            <tr v-for="(course, index) in courses" :key="index">
                <td>{{index + 1}}</td>
                <td>{{course.title}}</td>
                <td>{{course.semester}}</td>
                <td>{{course.grade}}</td>
            </tr>
            </tbody>
        </table>
        <br>
        <br>
        <div>
            <button id="add-course-button"
                    :class="{'blue-button' : !addButtonSelected, 'grey-button' : addButtonSelected}"
                    @click="selected = createFields(addButtonSelected)">+
            </button>
            <span id="add-course" :class="{'add-course-not-visible' : !addButtonSelected, 'add-course-visible' : addButtonSelected}">
                <input class="input" type="text" placeholder="Course title" id="title">
                <input class="input" type="number" min="1" max="8" placeholder="Semester" id="semester">
                <input class="input" type="number" min="0" max="100" placeholder="Grade" id="grade">
                <button class="green-button" id="save-course">Save</button>
                <button class="grey-button" id="cancel-course" @click="selected=cancel()">Cancel</button>
            </span>
        </div>
    </div>
</template>

<script>
    import Course from "../models/Course";

    export default {
        name: "Courses",

        data: () => {
            return {
                addButtonSelected: false
            }
        },
        methods: {
            // Probably useful?
            calculateGPA: function () {

            },
            addCourse: function (title, semester, grade) {
                let newCourse = new Course(title, semester, grade);
                this.courses.push(newCourse); // faulty
            },
            createFields: function (buttonSelected) {
                this.addButtonSelected = !buttonSelected;
            },
            cancel: function () {
                this.addButtonSelected = false;
            }
        },
        props: {
            courses: Array,
            coursesSelected: Boolean
        }
    }
</script>

<style scoped>

    table {
        width: 100%;
        border-collapse: collapse;

    }

    table th {
        padding: 8px 12px;
        text-align: left;
        border: 1px solid #cbcbcb;
        background-color: #03A9F4;
        color: #ffffff;
    }

    table td {
        padding: 8px 12px;
        border: 1px solid #cbcbcb;
    }

    .add-course-visible {
        display: inline;
    }

    .add-course-not-visible{
        display: none;
    }

    .green-button {
        background-color: #69f378;
        color: #ffffff;
        border: none;
        padding: 10px 10px;
    }

    .grey-button {
        background-color: #e1e8e6;
        color: #ffffff;
        border: none;
        padding: 10px 20px;
    }

    .blue-button {
        background-color: #2196F3;
        color: #ffffff;
        border: none;
        padding: 10px 20px;
    }

    .input {
        border: 1px solid #cccccc;
        padding: 10px 20px;
        min-width: 135px;
    }


</style>