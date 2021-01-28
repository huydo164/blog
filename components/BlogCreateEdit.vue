<template>
  <div class="data">
    <div class="form-group">
      <label class="bold">Tiêu đề</label>
      <input
        type="text"
        class="form-control"
        v-model="blogs.title"
      >
    </div>
    <div class="form-group">
      <label class="bold">Mô tả ngắn</label>
      <input
        type="text"
        class="form-control"
        v-model="blogs.des"
      >
    </div>
    <div class="form-group">
      <label class="bold">Chi tiết</label>
      <textarea
        class="form-control"
        rows="3"
        v-model="blogs.detail"
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
        v-model="blogs.category"
      >
        <option
          v-for="(cate,index) in data_cate"
          v-bind:key="cate"
          :value="index"
        >{{cate}}</option>
      </select>
    </div>
    <div class="form-group">
      <label class=" bold">Vị trí</label>
      <ul class="list-group list-group-flush">
        <li
          v-for="(pos, index) in data_pos"
          v-bind:key="pos"
          class="list-group-control"
        >
          <div class="custom-control custom-checkbox">
            <input
              type="checkbox"
              class="custom-control-input"
              :id="index + 'custom'"
              :value="index"
              name="vietnam"
              v-model="blogs.position"
            >
            <label
              class="custom-control-label"
              :for="index + 'custom'"
            >{{ pos }}</label>
          </div>
        </li>
      </ul>
    </div>
    <div class="form-group">
      <label class="bold">Public</label><br>
      <input
        type="radio"
        id="checkbox1"
        :name="yes"
        :value="true"
        v-model="blogs.public"
      >
      <label for="checkbox1">Yes</label><br>
      <input
        type="radio"
        id="checkbox2"
        :name="no"
        :value="false"
        v-model="blogs.public"
      >
      <label for="checkbox2">No</label><br>
    </div>
    <div class="form-group row">
      <label class="col-lg-12 bold">Date Public</label>
      <input
        type="date"
        class="form-control col-lg-3"
        v-model="blogs.data_pubblic"
      >
    </div>
    <div class="button">
      <button
        v-if="this.$route.name == 'create'"
        v-on:click="addData()"
        class="btn btn-success"
      >Submit</button>
      <button
        v-else
        v-on:click="updateData()"
        class="btn btn-success"
      >Submit</button>
      <button class="btn btn-primary">Clear</button>
    </div>
    <ul
      v-if="errors.length"
      class="alert alert-warning"
    >
      <li
        v-for="error in errors"
        v-bind:key="error"
      >{{error}}</li>
    </ul>
  </div>
</template>

<script>
import axios from "axios"
export default {
  data() {
    return {
      data_cate: ['thế giới', 'kinh tế', 'giải trí', 'bóng đá', 'chính trị'],
      data_pos: ['Việt Nam', 'Châu Âu', 'Châu Á', 'Châu Mỹ'],
      blogs: {
        id: '',
        title: '',
        des: '',
        detail: '',
        category: '',
        public: '',
        data_pubblic: '',
        position: [],
        thumbs: '',
      },
      errors: []
    }
  },
  created() {
    if (this.$route.name != 'create') {
      this.listData()
    }
  },
  methods: {
    addData() {
      this.errors = []
      if (this.blogs.title == '') {
        this.errors.push('title không được trống')
      }
      if (this.blogs.des == '') {
        this.errors.push('des không được trống')
      }
      if (this.blogs.detail == '') {
        this.errors.push('deatil không được trống')
      }
      if (this.blogs.category == '') {
        this.errors.push('category không được trống')
      }
      if (this.blogs.public == '') {
        this.errors.push('public không được trống')
      }
      if (this.blogs.data_pubblic == '') {
        this.errors.push('data_pubblic không được trống')
      }
      if (this.errors.length > 0) {
        return false
      }
      else {
        axios.post('http://localhost:4000/blogs', this.blogs).then(function (response) { });
      }
    },

    listData() {
      axios.get('http://localhost:4000/blogs/' + this.$route.params.id).then((response) => {
        this.blogs = response.data
      })
    },

    updateData() {
      axios.put('http://localhost:4000/blogs/' + this.$route.params.id, this.blogs).then(function (response) { })
    }
  }
}
</script>