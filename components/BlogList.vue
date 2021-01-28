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
          <td v-if="blog.category == 0">Xã hội</td>
          <td v-else-if="blog.category == 1">Thế giới</td>
          <td v-else-if="blog.category == 2">Kinh tế</td>
          <td v-else-if="blog.category == 3">Giải trí</td>
          <td v-else-if="blog.category == 4">Bóng đá</td>
          <td v-else-if="blog.category == 5">Chính trị</td>
          <td v-else>Đời sống</td>
          <td v-if="blog.public == true">Yes</td>
          <td v-if="blog.public == false">No</td>
          <td>
            <ul>
              <div
                v-for="position of blog.position"
                v-bind:key="position"
              >
                <li v-if="position == 1"> Hà Nội</li>
                <li v-if="position == 2"> Châu Âu</li>
                <li v-if="position == 3"> Châu Á</li>
                <li v-if="position == 4"> Châu Mỹ</li>
              </div>
            </ul>
          </td>
          <td>{{blog.data_pubblic}}</td>
          <td><a
              v-bind:href="/edit/ + blog.id"
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
export default {
  props: ['blogs'],

  methods: {
    doDelete(id, index) {
      axios.delete('http://localhost:4000/blogs/' + id).then((response) => {
        this.blogs.splice(index, 1)
      })
    },
  }
}
</script>