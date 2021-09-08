<template>
  <div class="hello">
        <h1>COURSES</h1>
        <table cellspacing='0' class="table">
            <tr v-for="(course, index) in courses" :key="index">
                <strong><td>{{ course.name }}</td></strong>
                <td>
                  <strong><router-link :to="{ name: 'Courses', params: { name: course.name } }">View</router-link></strong>
                </td>
            </tr>
        </table>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  // props: {
  //   msg: String
  // },
  computed: {
    courses() {
      return this.$store.getters.courses
    }
  }
}
</script>


<style lang="scss">
  .hello {
    table{
      display: inline;
      margin-left: auto;
      margin-right: auto;
    }
  }
</style>