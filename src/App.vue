<template>
  <div id="app" class="d-flex flex-column min-vh-100">
    <!-- Main Content -->
    <main class="flex-fill">
      <div class="container-fluid">
        <div class="row mb-5">
          <h1>Degree Planner</h1>
        </div>
        <div class="row main-content">
          <!-- Classes -->
          <div class="col-lg-4 required-classes">
            <h3>Required Classes</h3>

            <b-tabs content-class="mt-3">
              <!-- LAC Requirements -->

              <b-tab title="LAC" active>
                <div id="lac">
                  <div class="my-4 text-left" id="lac-reqs">
                     <CourseInfo :course=course v-for="course in lacCourses" :key="course.id" @add-class="addClass" />
                  </div>
                </div>
              </b-tab>

              <b-tab title="CS">
                <div id="cis">
                  <div class="my-4 text-left" id="cis-reqs">
                    <CourseInfo :course=course v-for="course in cisCourses" :key="course.id" @add-class="addClass" />
                  </div>
                </div>
              </b-tab>

               <b-tab title="CYB">
                <div id="cyb">
                  <div class="my-4 text-left" id="cyb-reqs">
                    <CourseInfo :course=course v-for="course in cybCourses" :key="course.id" @add-class="addClass" />
                  </div>
                </div>
              </b-tab>
            </b-tabs>
          </div>

          <!-- Semester Schedules -->
          <div class="col-lg-6 semester-schedules">
            <h3>Semester Schedules</h3>

            <SemesterSchedule
            :semester=schedule
              v-for="schedule in schedules"
              :key="schedule.id"
              class="accordion my-4"
              id="schedule.id"
              @remove-course="remove"
            />
             
          </div>

          <!-- Table of Contents Sidebar -->
          <div class="col-lg-2 position-sticky top-0 h-100 ps-5 toc">
            <nav>
              <p class="text-muted">On this page</p>
              <ul>
                <li><a href="#fall2020">Fall 2020</a></li>
                <li><a href="#spring2021">Spring 2021</a></li>
                <li><a href="#fall2021">Fall 2021</a></li>
                <li><a href="#spring2022">Spring 2022</a></li>
                <li><a href="#fall2022">Fall 2022</a></li>
                <li><a href="#spring2023">Spring 2023</a></li>
                <li><a href="#fall2023">Fall 2023</a></li>
                <li><a href="#spring2024">Spring 2024</a></li>
              </ul>
            </nav>
          </div>
        </div>
      </div>
    </main>

    <!-- Footer -->
    <footer class="bg-dark text-light py-4">
      <div class="container-fluid">
        <div class="row">
          <div class="col">
            <p>Made with ❤️ by FHU students!</p>
          </div>

          <div class="col-md-3">
            <p>&copy; 2021 Freed-Hardeman University</p>
          </div>
        </div>
      </div>
    </footer>
  </div>
</template>

<script>
import CourseInfo from "./components/CourseInfo.vue"
import SemesterSchedule from "./components/SemesterSchedule.vue"
import lacCourses from "./lac.json"
import cisCourses from "./cis.json"
import cybCourses from "./cyb.json"
//import HelloWorld from './components/HelloWorld.vue'
export default {
  name: "App",
  components: {
    CourseInfo,
    SemesterSchedule
    //HelloWorld
  },
  methods: {
    addClass(id, value) {
      let class1 = {};
      this.cisCourses.forEach(c => {
        if (c.id == id) {
          class1 = c;
        }
      })
      this.lacCourses.forEach(c => {
        if (c.id == id) {
          class1 = c;
        }
      })
      this.cybCourses.forEach(c => {
        if (c.id == id) {
          class1 = c;
        }
      })
      this.schedules.forEach( s => 
      {
        if (s.id == value) {
          if (!s.classes.includes(class1)) {
          s.classes.push(class1);
        }
        }
        }
      )
    },
    remove(id, semester) {
      let class1 = {};
      this.cisCourses.forEach(c => {
        if (c.id == id) {
          class1 = c;
        }
      })
      this.lacCourses.forEach(c => {
        if (c.id == id) {
          class1 = c;
        }
      })
      this.cybCourses.forEach(c => {
        if (c.id == id) {
          class1 = c;
        }
      })
      this.schedules.forEach( s => 
      {
        if (s.id == semester) {
          if (s.classes.includes(class1)) {
          s.classes.pop(class1);
        }
        }
        }
      )
    }
  },
  data() {
    return {
      lacCourses: lacCourses,
      cisCourses: cisCourses,
      cybCourses: cybCourses,
      schedules: [
        {
          name: "Fall 2020",
          id: "fall2020",
          collapseId: "fall2020schedule",
          classes: [],
        },
        {
          name: "Spring 2021",
          id: "spring2021",
          collapseId: "spring2021schedule",
          classes: [],
        },
        {
          name: "Fall 2021",
          id: "fall2021",
          collapseId: "fall2021schedule",
          classes: [],
        },
        {
          name: "Spring 2022",
          id: "spring2022",
          collapseId: "spring2022schedule",
          classes: [],
        },
        {
          name: "Fall 2022",
          id: "fall2022",
          collapseId: "fall2022schedule",
          classes: [],
        },
        {
          name: "Spring 2023",
          id: "spring2023",
          collapseId: "spring2023schedule",
          classes: [],
        },
        {
          name: "Fall 2023",
          id: "fall2023",
          collapseId: "fall2023schedule",
          classes: [],
        },
        {
          name: "Spring 2024",
          id: "spring2024",
          collapseId: "spring2024schedule",
          classes: [],
        },
      ],
    };
  },
};
</script>

<style>
#app {
  font-family: "Nunito Sans", sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}

.toc nav {
  text-align: left;
}

.toc ul {
  padding: 0;
  list-style: none;
}

.toc li {
  margin: 0;
  margin-bottom: 0.5rem;
}

.toc li a {
  text-decoration: none;
}

.toc li a:hover {
  text-decoration: underline;
}

.required-classes .card {
  border-left: 8px solid #0c63e4;
}
</style>
