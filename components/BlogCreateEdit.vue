<template>
    <div class="data">
            <div class="form-group">
                <label class="bold">Tiêu đề</label>
                <input type="text" class="form-control" v-model="blogs.title">
            </div>
            <div class="form-group">
                <label class="bold">Mô tả ngắn</label>
                <input type="text" class="form-control" v-model="blogs.des">
            </div>
            <div class="form-group">
                <label class="bold">Chi tiết</label>
                <textarea class="form-control" rows="3" v-model="blogs.detail"></textarea>
            </div>
            <div class="form-group">
                <label class="bold">Hình ảnh</label><br>
                <input type="file" name="fileUpload">
            </div>
            <div class="form-group row">
                <label class="col-lg-12 bold">Loại</label>
                <select class="form-control custom-select col-lg-2" v-model="blogs.category">
                    <option value="0">Xã hội</option>
                    <option value="1">Thế giới</option>
                    <option value="2">Kinh tế</option>
                    <option value="3">Giải trí</option>
                </select>
            </div>
            <div class="form-group">
                <ul class="list-group list-group-flush">
                    <li class="list-group-control">
                        <div class="custom-control custom-checkbox">
                            <input type="checkbox" class="custom-control-input" id="customCheck1" value="1" name="vietnam" v-model="blogs.position">
                            <label class="custom-control-label" for="customCheck1">Hà Nội</label>
                        </div>
                    </li>
                    <li class="list-group-control">
                        <div class="custom-control custom-checkbox">
                            <input type="checkbox" class="custom-control-input" id="customCheck2" value="2" name="chaua" v-model="blogs.position">
                            <label class="custom-control-label" for="customCheck2">Châu Âu</label>
                        </div>
                    </li>
                    <li class="list-group-control">
                        <div class="custom-control custom-checkbox">
                            <input type="checkbox" class="custom-control-input" id="customCheck3" value="3" name="chauau" v-model="blogs.position">
                            <label class="custom-control-label" for="customCheck3">Châu Á</label>
                        </div>
                    </li>
                    <li class="list-group-control">
                        <div class="custom-control custom-checkbox">
                            <input type="checkbox" class="custom-control-input" id="customCheck4" value="4" name="chaumy" v-model="blogs.position">
                            <label class="custom-control-label" for="customCheck4">Châu Mỹ</label>
                        </div>
                    </li>
                </ul>
            </div>
            <div class="form-group">
                <label class="bold">Public</label><br>
                <input type="radio" id="checkbox1" name="yes" value="true" v-model="blogs.public">
                <label for="checkbox1">Yes</label><br>
                <input type="radio" id="checkbox2" name="no" value="false" v-model="blogs.public">
                <label for="checkbox2">No</label><br>
            </div>
            <div class="form-group row">
                <label class="col-lg-12 bold">Date Public</label>
                <input type="date" class="form-control col-lg-3" >
            </div>
            <div class="button">
                <button v-on:click="submit()" class="btn btn-success">Submit</button>
                <button class="btn btn-primary">Clear</button></button>
            </div>
    </div>
</template>

<script>
import axios from "axios"
export default {
    data(){
        return {
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
            }
        }
    },
    methods:{
        submit(){
            axios.post('http://localhost:4000/blogs', this.blogs).then(function(response){

            }.bind(this));
        }
    }
}
</script>