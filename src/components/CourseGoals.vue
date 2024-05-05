<template>
  <div>
    <goals-list :goals="filteredGoals"></goals-list>
    <add-goal @add-goal="addGoal"></add-goal>
  </div>
</template>

<script>
import GoalsList from './GoalsList.vue'
import AddGoal from './AddGoal.vue'
import { computed, ref } from 'vue'

export default {
  components: {
    GoalsList,
    AddGoal
  },

  setup() {
    const goals = ref([])

    const filteredGoals = computed(function () {
      return goals.value.filter(
        (goal) => !goal.text.includes('Angular') && !goal.text.includes('React')
      )
    })

    const addGoal = (text) => {
      const newGoal = {
        id: new Date().toISOString(),
        text: text
      }
      goals.value.push(newGoal)
    }

    return { filteredGoals, addGoal }
  }
}
</script>
