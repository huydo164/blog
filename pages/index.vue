<template>
  <div>
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
  </div> 
</template>

<script>
import AppMenu from '@/components/AppMenu'
import BlogList from '@/components/BlogList'
export default {
  layout: "default"
}
</script>