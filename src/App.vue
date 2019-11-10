<template>
    <main id="app">
        <header>
            <strong>Welcome to your dashboard!</strong>
        </header>
        <section id="container">
            <section id="main">

                <div class="content">
    
                    <Profile :user="user" :profileSelected="profileSelected"/>
                    <Courses :courses="courses" :coursesSelected="coursesSelected"/>
                </div>

                <div class="controls">
                    <button id="profile-button" :class="{'pill active' : profileSelected, 'pill' : !profileSelected}" @click="swapViews('profile-button', profileSelected)">Profile</button>
                    <button id="courses-button" :class="{'pill active' : coursesSelected, 'pill' : !coursesSelected}" @click="swapViews('courses-button', coursesSelected)">Courses</button>
                </div>

            </section>
        </section>
        <footer>
            <ul class="links">
                <li>
                    <a href="https://ois2.ut.ee/" target="_blank">OIS</a>
                </li>
                <li>
                    <a href="https://courses.cs.ut.ee/" target="_blank">Courses</a>
                </li>
            </ul>
        </footer>
    </main>
</template>

/* Maybe create components for footer and header as well */

<script>

    import Courses from "./components/Courses";
    import Profile from "./components/Profile";
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
            Courses
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

    header {
        padding: 20px;
        background-color: #2196F3;
        color: #ffffff;
        text-align: center;
        margin-bottom: 10px;
        height: 60px;
    }

    footer {
        padding: 30px 0;
        background-color: #607D8B;
        margin-top: 10px;
        height: 100px;
        position: absolute;
        bottom: 0;
        width: 100%;
    }

    footer .links {
        display: block;
        width: 100%;
        max-width: 200px;
        margin: 0 auto;
        color: #acd7ff;
        font-size: 11px;
    }

    footer .links a {
        text-decoration: none;
        color: #acd7ff;
    }

    footer .links a:hover {
        text-decoration: underline;
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
