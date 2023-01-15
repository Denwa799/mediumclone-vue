<template>
  <app-topbar />
  <router-view />
</template>

<script>
import AppTopbar from '@/components/Topbar'

export default {
  name: 'App',
  components: {
    AppTopbar
  }
}
</script>