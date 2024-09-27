<template>
  <div>
    <UserDashboard :userData="user" />
  </div>
</template>

<script>
import UserDashboard from '@/components/UserDashboard.vue'
import { useUserStore } from '@/stores/user'

export default {
  setup() {
    const userStore = useUserStore()
    const user = userStore.user

    return {
      user
    }
  },
  components: {
    UserDashboard
  }
}
</script>
