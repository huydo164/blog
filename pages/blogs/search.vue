<template>
  <div>
    <div class="container">
      <div class="row">
        <div class="col-lg-3">
          <app-menu></app-menu>
        </div>
        <div class="col-lg-9">
          <div class="form-search">
            <h3>Search Blogs</h3>

            <div class="form-group row">
              <label class="col-sm-2 col-form-label">
                Tiêu đề
              </label>
              <div class="col-sm-10">
                <input
                  class="form-control"
                  placeholder="Tìm kiếm.."
                  v-model="search"
                >
              </div>
            </div>
            <button
              class="btn btn-success"
              @click="searchData(search)"
            >Search</button>

          </div>
          <blog-list :blogs="blogs"></blog-list>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import BlogList from '@/components/BlogList'
import axios from "axios"
export default {
  components: { BlogList },
  data() {
    return {
      search: '',
      blogs: []
    }
  },

  mounted() {
    this.searchData(this.search)
  },

  methods: {
    searchData: function (search = "") {
      const url = search ? 'http://127.0.0.1:8000/api/blogs?title_like=' + search : 'http://127.0.0.1:8000/api/blogs';
      axios.get(url).then((response) => {
        this.blogs = response.data
      })
    }
  }
}
</script>