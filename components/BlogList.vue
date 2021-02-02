<template>
  <div class="list-data">
    <h2>List Blogs</h2>
    <table class="table table-hover table-bordered">
      <thead class="thin-border-bottom">
        <tr>
          <th>ID</th>
          <th>Tin</th>
          <th>Loại</th>
          <th>Trạng thái</th>
          <th>Vị trí</th>
          <th>Ngày Public</th>
          <th>Edit</th>
          <th>Delete</th>
        </tr>
      </thead>
      <tbody v-if="blogs && blogs.length">
        <tr
          v-for="(blog, index) in blogs"
          v-bind:key="blog.id"
        >
          <td>{{blog.id}}</td>
          <td>{{blog.title}}</td>
          <td>{{findCategory(blog.category)}}</td>
          <td v-if="blog.public == 1 ">Yes</td>
          <td v-if="blog.public == 2 ">No</td>
          <td>
            <p>{{parseJSONIfJSON(blog.position)}}</p>
          </td>
          <td>{{blog.data_pubblic}}</td>
          <td><a v-bind:href=" '/blogs/' +blog.id">Edit</a></td>
          <td><button
              type="button"
              class="btn btn-danger"
              @click="doDelete(blog.id, index)"
            >Delete</button></td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import axios from "axios"
import { CATEGORY_LIST } from '@/mockdata/mock'
import { POSITION_LIST } from '@/mockdata/mock'
export default {
  props: ['blogs'],

  data() {
    return {
      CATEGORY_LIST,
      POSITION_LIST,
    }
  },

  computed: {

  },

  methods: {
    doDelete(id, index) {
      axios.delete('http://127.0.0.1:8000/api/blogs/' + id).then((response) => {
        this.blogs.splice(index, 1)
      })
    },
    parseJSONIfJSON(posit) {
      try {
        const posArr = JSON.parse(posit)
        return posArr.join(', ')
      } catch (error) {
        return ""
      }
    },

    findCategory(id) {
      const category = CATEGORY_LIST.find(element => element === id)
      return category ? category : ''
    }
  }
}
</script>