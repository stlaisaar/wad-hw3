<template>
    <main id="app">
        <Header/>
        <section id="container">
            <section id="main">

                <div class="content">
    
                    <Profile :user="user" :profileSelected="profileSelected" :gpa="calculateGPA()"/>
                    <Courses :courses="courses" :coursesSelected="coursesSelected" :user="user"/>
                </div>

                <div class="controls">
                    <button id="profile-button" :class="{'pill active' : profileSelected, 'pill' : !profileSelected}" @click="swapViews('profile-button', profileSelected)">Profile</button>
                    <button id="courses-button" :class="{'pill active' : coursesSelected, 'pill' : !coursesSelected}" @click="swapViews('courses-button', coursesSelected)">Courses</button>
                </div>

            </section>
        </section>
        <Footer/>
    </main>
</template>

<script>

    import Courses from "./components/Courses";
    import Profile from "./components/Profile";
    import Footer from "./components/Footer";
    import Header from "./components/Header";
    import User from "./models/User";
    import Course from "./models/Course";

    export default {
        name: 'app',

        data: () => {
            let user = new User(
                "Jane",
                "Boe",
                "13/12/1911",
                "Software Development",
                "5.0"
                
            );
            return {
                
                user,
                courses: [
                    new Course("Programming", 1, 95),
                    new Course("OOP", 2, 83),
                    new Course("Databases", 2, 89),
                    new Course("Discrete mathematics", 3, 61),
                ],
                profileSelected: true,
                coursesSelected: false
            }
        },
        methods: {
            calculateGPA: function () {
                var sum = 0;
                this.courses.forEach(e => {
                    if(e.grade>=90){
                        sum+=4
                    }
                    else if(e.grade>=80&&e.grade<90){
                        sum+=3
                    }
                    else if(e.grade>=70&&e.grade<80){
                        sum+=2
                    }
                    else if(e.grade>=60&&e.grade<70){
                        sum+=1
                    }
                    else if(e.grade>=50&&e.grade<60){
                        sum+=0.5
                    }
                    else if(e.grade<=50){
                        sum+=0
                    }
                    else {
                        sum+=0
                    }
                });
                return (Math.round(((sum)/this.courses.length) * 100)/100)
            },
            swapViews: function (id, buttonAlreadySelected) {
                /* eslint-disable no-console */
                console.log(id);
                // Courses button was pressed, Courses component currently not being shown, show Courses component
                if (id === "courses-button" && buttonAlreadySelected === false) {
                    this.profileSelected = false;
                    this.coursesSelected = true;
                }
                // Profile button was pressed, Profile component currently not being shown, show Profile component
                else if (id === "profile-button" && buttonAlreadySelected === false) {
                    this.coursesSelected = false;
                    this.profileSelected = true;
                }
            }

        },
        components: {
            Profile,
            Courses,
            Footer,
            Header
        }
    }
</script>

<style>
    * {
        box-sizing: border-box;
        font-family: 'Livvic', sans-serif;
    }

    html, body {
        padding: 0;
        margin: 0;
        width: 100%;
        height: 100%;
        background-color: #eaeaea;
    }

    main {
        position: relative;
        min-height: 100%;
        padding-bottom: 110px;
    }

    .clear-fix {
        clear: both;
    }

    #container {
        width: 80%;
        max-width: 900px;
        min-width: 320px;
        padding: 15px;
        background-color: #ffffff;
        margin: 0 auto;
    }

    .content {
        padding: 10px;
        border: 1px solid #cbcbcb;
    }

    .content .tab {
        display: none;
    }

    .content .tab.active {
        display: block;
    }

    .controls .pill {
        border: 1px solid #cbcbcb;
        background-color: #eaeaea;
        padding: 10px;
        border-bottom-left-radius: 4px;
        border-bottom-right-radius: 4px;
        border-top: none;
        margin-top: -1px;
        outline: none !important;
    }

    .controls .pill.active {
        background-color: #ffffff;
        border-top: 1px solid #ffffff;
    }

    .controls .pill:hover {
        cursor: pointer;
    }

</style>
