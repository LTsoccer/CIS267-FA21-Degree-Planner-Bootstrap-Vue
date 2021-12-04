<template>
              <div class="accordion-item">
                <h2
                  class="accordion-header"
                  id="fall2019heading"
                  v-b-toggle:[semester.collapseId]
                >
                  <div class="changes" :id="semester.id" @click="change">
                    <h4 class="my-0 change1">{{ semester.name }}</h4>
                    <span class="changing" v-if="before" >⯆</span>
                    <span class="changing" v-if="!before" >⯅</span>
                  </div>
                </h2>
                <b-collapse :id="semester.collapseId">
                  <div class="accordion-body">
                    <table class="table table-hover table-striped">
                      <thead>
                        <th scope="col">Course</th>
                        <td scope="col"></td>
                        <td scope="col"></td>
                        <th scope="col">Credits</th>
                      </thead>
                      <tr v-for="course in semester.classes" :course=course :key="course.id" @click="remove(course.id, semester.id)">
                        <td>{{course.id}}</td>
                        <td>
                          <span class="fw-bold"> {{course.name}} </span>
                        </td>
                        <td>
                          <span class="badge bg-primary"> {{course.badge}} </span>
                        </td>
                        <td>{{course.hours}}</td>
                      </tr>
                      <tr>
                        <th>Total Hours</th>
                        <td></td>
                        <td></td>
                        <th>{{semester.total}}</th>
                      </tr>
                    </table>
                  </div>
                </b-collapse>
              </div>
</template>

<script>
export default {
    name: 'SemesterSchedule',
    props: {
        semester: Object
    },
    data () {
      return {
        before: true
      }
    },
    methods: {
      change() {
        if (this.before == true) {
          this.before = false;
        }
        else {
          this.before = true;
        }
      },
        remove(id, semester) {
            this.$emit("remove-course", id, semester);
        }
    }

}
</script>

<style>
.changes {
  display: flex;
}
.change1 {
  flex-basis: 75%;
}
.changing {
  flex-basis: 25%;
  justify-content: space-between;
  text-align: right;
}
</style>