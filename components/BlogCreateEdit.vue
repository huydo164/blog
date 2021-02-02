<template>
  <div class="data">
    <div class="form-group">
      <label class="bold">Tiêu đề</label>
      <input
        type="text"
        class="form-control"
        v-model="blog.title"
      >
    </div>
    <div class="form-group">
      <label class="bold">Mô tả ngắn</label>
      <input
        type="text"
        class="form-control"
        v-model="blog.des"
      >
    </div>
    <div class="form-group">
      <label class="bold">Chi tiết</label>
      <textarea
        class="form-control"
        rows="3"
        v-model="blog.detail"
      ></textarea>
    </div>
    <div class="form-group">
      <label class="bold">Hình ảnh</label><br>
      <input
        type="file"
        name="fileUpload"
      >
    </div>
    <div class="form-group row">
      <label class="col-lg-12 bold">Loại</label>
      <select
        class="form-control custom-select col-lg-2"
        v-model="blog.category"
      >
        <option
          v-for="(cate,index) in CATEGORY_LIST"
          :key="cate"
          :value="index"
        >{{cate}}</option>
      </select>
    </div>
    <div class="form-group">
      <p>Vị trí</p>
      <ul class="list-group list-group-flush">
        <li
          v-for="(post,key) in POSITION_LIST"
          :key="post"
          class="list-group-control"
        >
          <div class="custom-control custom-checkbox">
            <input
              type="checkbox"
              :value="post"
              class="custom-control-input"
              :id="'check' + key + 1"
              v-model="blog.position"
            >
            <label
              class="custom-control-label"
              :for=" 'check' + key + 1 "
            >{{ post }}</label>
          </div>
        </li>
      </ul>
    </div>
    <div class="form-group">
      <label class="bold">Public</label><br>
      <input
        type="radio"
        id="checkbox1"
        name="public"
        :value=1
        v-model="blog.public"
      >
      <label for="checkbox1">Yes</label><br>
      <input
        type="radio"
        id="checkbox2"
        name="public"
        :value=2
        v-model="blog.public"
      >
      <label for="checkbox2">No</label><br>
    </div>
    <div class="form-group row">
      <label class="col-lg-12 bold">Date Public</label>
      <input
        type="date"
        class="form-control col-lg-3"
        v-model="blog.data_pubblic"
      >
    </div>
    <div class="button">
      <button
        v-if="this.$route.name == 'blogs-create'"
        v-on:click="addData()"
        class="btn btn-success"
      >Add</button>
      <button
        v-else
        v-on:click="updateData()"
        class="btn btn-success"
      >Update</button>
      <button class="btn btn-primary">Clear</button>
    </div>
    <div v-if="errors && errors.length ">
      <li
        v-for="error in errors"
        :key="error"
      >
        <p class="alert alert-warning">{{ error }}</p>
      </li>
    </div>
  </div>
</template>

<script>
import axios from "axios"
import { CATEGORY_LIST } from '@/mockdata/mock'
import { POSITION_LIST } from '@/mockdata/mock'
export default {
  props: {
  },
  data() {
    return {
      CATEGORY_LIST,
      POSITION_LIST,
      blog: {
        title: '',
        des: '',
        detail: '',
        category: '',
        public: '',
        data_pubblic: '',
        position: [],
      },
      errors: [],
    }
  },

  mounted() {
    if (this.$route.name !== 'blogs-create') {
      this.listData()
    }
  },

  methods: {
    addData() {
      this.errors = [];
      Object.entries(this.blog).forEach(([key, value]) => {
        console.log(key, value)
        if (!value) {
          this.errors.push(key + ' Rỗng')
        }
      })
      if (!this.errors.length) {
        this.blog.position = JSON.stringify(this.blog.position)
        axios.post('http://127.0.0.1:8000/api/blogs', this.blog).then(function (response) { }.bind(this)).then(
          () => {
            this.$router.push({ path: '/blogs' })
          }
        );
      }
    },

    listData() {
      axios.get('http://127.0.0.1:8000/api/blogs/' + this.$route.params.id).then((response) => {
        const blog = response.data
        blog.position = JSON.parse(blog.position)
        this.blog = blog
      })
    },

    updateData() {
      this.errors = []
      if (this.blog.title == '') {
        this.errors.push('title không được trống')
      }
      if (this.blog.des == '') {
        this.errors.push('des không được trống')
      }
      if (this.blog.detail == '') {
        this.errors.push('deatil không được trống')
      }
      if (this.blog.category == '') {
        this.errors.push('category không được trống')
      }
      if (this.blog.public == '') {
        this.errors.push('public không được trống')
      }
      if (this.blog.data_pubblic == '') {
        this.errors.push('data_pubblic không được trống')
      }
      if (this.blog.position == []) {
        this.errors.push('position không được trống!')
      }
      if (this.errors.length > 0) {
        return false
      }
      else {
        this.blog.position = JSON.stringify(this.blog.position)
        axios.put('http://127.0.0.1:8000/api/blogs/' + this.$route.params.id, this.blog)
          .then(function (response) {
          }.bind(this)).then(
            () => {
              this.$router.push({ path: '/blogs' })

            }
          );
      }
    }
  }
}
</script>