<template>
  <div>
    <app-header></app-header>
    <nuxt />
    <app-footer></app-footer>
  </div>
</template>
<script>
import AppHeader from '@/components/AppHeader'
import AppFooter from '@/components/AppFooter'
export default {
  components:{
    AppHeader,AppFooter
  }
}
</script>