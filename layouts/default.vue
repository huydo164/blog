<template>
  <div>
    <app-header></app-header>
    <div class="content">
      <div class="container">
          <div class="row">
            <div class="col-lg-3">
              <app-menu></app-menu>
            </div>
            <div class="col-lg-9">
              <blog-list></blog-list>
            </div>
          </div>
    </div>
    </div>
    <app-footer></app-footer>
  </div>
</template>
<script>
import AppHeader from '@/components/AppHeader'
import AppMenu from '@/components/AppMenu'
import BlogList from '@/components/BlogList'
import AppFooter from '@/components/AppFooter'
export default {
  components:{
    AppHeader, AppMenu, BlogList,AppFooter
  }
}
</script>