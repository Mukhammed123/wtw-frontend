<!-- src/views/DashboardPage.vue -->
<template>
  <div>
    <UserDashboard :userData="userData" />
  </div>
</template>

<script>
import UserDashboard from '@/components/UserDashboard.vue'

export default {
  data() {
    return {
      userData: {
        id: 1,
        first_name: 'TestUser'
      }
    }
  },
  components: {
    UserDashboard
  }
}
</script>
