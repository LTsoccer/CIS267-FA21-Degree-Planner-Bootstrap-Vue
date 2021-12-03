<template>
              <div class="accordion-item">
                <h2
                  class="accordion-header"
                  id="fall2019heading"
                  v-b-toggle:[semester.collapseId]
                >
                  <div :id="semester.id">
                    <h4 class="my-0">{{ semester.name }}</h4>
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
                      <tr v-for="course in semester.classes" :key="course.id" @click="remove(course.id, semester.id)">
                        <td>{{course.id}}</td>
                        <td>
                          <span class="fw-bold"> {{course.name}} </span>
                        </td>
                        <td>
                          <span class="badge bg-primary"> {{course.badge}} </span>
                        </td>
                        <td>{{course.hours}}</td>
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
    methods: {
        remove(id, semester) {
            this.$emit("remove-course", id, semester);
        }
    }

}
</script>

<style>

</style>