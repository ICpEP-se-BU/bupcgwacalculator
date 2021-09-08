<template>
  <div class="container">
      <h1>COMPUTE YOUR GRADES HERE</h1>
      <ul v-for="subs in findSemYear.subjects" :key="subs.sub">
          <li>{{ subs.sub }} <input type="number" name="" id="" v-model="subs.grades"> </li>
      </ul>
      <h1 class="gwa">{{ total }}</h1>
      <button @click="computedGWA" class="compute-btn" >Compute</button>
  </div>
</template>

<script>
export default {
    name: 'Compute',
    computed: {
        findSemYear() {
            return this.$store.getters.findSemYear((parseInt(this.$route.params.id)), this.$route.params.name )
        }
    },
    data() {
        return{
            data: this.$store.state.courses.find(course => course.name == this.$route.params.name).Obj.find(course => course.id == this.$route.params.id).subjects,
            total: 'your GWA is...'
        }
    },
    methods: {
            computedGWA: function() {

            /* Trying to use ES6 Reduce for a more elegant code**/

               let gradesTimesUnits = 0
               

                for (let i in this.data) {
                    //This if loop is to make all no entries 0 so that the users can see their tentative GWA
                    if (this.data[i].grades === '') {
                        this.data[i].grades = "0"
                        this.data[i].units = "0"
                    }
                    gradesTimesUnits += (parseFloat(this.data[i].grades) * parseFloat(this.data[i].units))
                }

                const totalUnits = Object.values(this.data).reduce((a, {units}) => a + parseFloat(units) ,0)

                return this.total = (gradesTimesUnits/totalUnits).toFixed(3)

            }
        }
}
</script>

<style lang="scss">
    ul {
        list-style: none;
    }

    .gwa {
        color: rgb(126, 126, 126);
    }

    .compute-btn {
        padding: 10px 20px;
        background-color:rgb(7, 44, 146);
        border: none;
        color: white;
        border-radius: 15px ;
        cursor: pointer;
    }
</style>