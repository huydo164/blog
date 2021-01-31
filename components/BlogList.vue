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
          <td>
            <div
              v-for="(cate, key) in dataCate"
              :key="key"
            >
              <p v-if="key == blog.category">{{cate}}</p>

            </div>
          </td>
          <td v-if="blog.public == 1 ">Yes</td>
          <td v-if="blog.public == 2 ">No</td>
          <td>
            <ul>
              <div
                v-for="(posit) of blog.position"
                v-bind:key="posit"
              >
                <li
                  v-for="(pos, key ,index) in dataPos"
                  :key="index"
                >
                  <p v-if="key == posit">{{pos}}</p>
                </li>
              </div>
            </ul>
          </td>
          <td>{{blog.data_pubblic}}</td>
          <td><a
              v-bind:href=" '/blogs/' +blog.id"
              title=""
            >Edit</a></td>
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
import { DATA_CATE } from '@/constants/constants.js'
import { DATA_POS } from '@/constants/constants.js'
export default {
  props: ['blogs'],

  data() {
    return {
      DATA_CATE: DATA_CATE,
      DATA_POS: DATA_POS,
    }
  },

  computed: {
    dataCate: function () {
      return this.DATA_CATE
    },

    dataPos: function () {
      return this.DATA_POS
    }
  },

  methods: {
    doDelete(id, index) {
      axios.delete('http://127.0.0.1:8000/api/blogs/' + id).then((response) => {
        this.blogs.splice(index, 1)
      })
    },
  }
}
</script>