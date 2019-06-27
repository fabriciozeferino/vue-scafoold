<template>
  <div class="notification-bar -shadow" :class="notificationTypeClass">
    <p>{{ notification.message }}</p>
  </div>
</template>

<script>
import { mapActions } from 'vuex'

export default {
  props: {
    notification: {
      type: Object,
      required: true
    }
  },
  data() {
    return {
      timeout: null
    }
  },
  computed: {
    notificationTypeClass() {
      return `-text-${this.notification.type}`
    }
  },
  mounted() {
    this.timeout = setTimeout(() => this.remove(this.notification), 5000)
  },
  methods: mapActions('notification', ['remove']),
  beforeDestroy() {
    clearTimeout(this.timeout)
  }
}
</script>

<style scoped>
.notification-bar {
  padding: 0.15rem 1.25rem;
  margin-bottom: 5px;
  border-radius: 0.25rem;
  transition: all 0.2s linear;
  background-color: white;
  cursor: pointer;
}

.notification-bar:hover {
  transform: scale(1.01);
  box-shadow: 0 3px 12px 0 rgba(0, 0, 0, 0.2), 0 1px 15px 0 rgba(0, 0, 0, 0.19);
}
</style>
