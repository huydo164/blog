<template>
  <div>
    <div class="content">
      <div class="container">
        <div class="row">
          <div class="col-lg-3">
            <app-menu></app-menu>
          </div>
          <div class="col-lg-9">
            <blog-list :blogs="blogs" />
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import BlogList from '@/components/BlogList'
import axios from "axios"
export default {
  props: {
  },
  components: { BlogList },
  data() {
    return {
      blogs: []
    }
  },
  mounted() {
    this.listData()
  },
  methods: {
    listData: function () {
      const url = 'http://localhost:4000/blogs'
      axios.get(url).then((response) => {
        this.blogs = response.data
      })
    }
  },
}
</script>