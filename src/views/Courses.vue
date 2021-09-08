<template>
  <div class="container">
      <h1>{{ $route.params.name }}</h1>
       <div v-if="findCourse">
            <div class="one" v-for="one in findCourse.Obj" :key="one.id">
                <h3>{{ one.year }} YEAR {{ one.sem }} SEM </h3>
                    <div class="two" v-for="two in one.subjects" :key="two.id">
                        {{ two.sub }}
                    </div>
                    <strong><router-link :to="{ name: 'Compute', params: { id: one.id}}">View</router-link></strong>
            </div>
        </div>
  </div>
 
</template>

<script>
export default {
    name: 'Courses',
    computed: {
        findCourse() {
            return this.$store.getters.findCourse(this.$route.params.name)
        }
    }
}
</script>

<style>
    .one {
        margin-bottom: 20px;
        margin-top: 20px;
    }

    strong {
        font-size: 20px;
    }
</style>