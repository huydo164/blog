<template>
    <div class="data">
        <form method="post" action="" enctype="multipart/form-data">
            <div class="form-group">
                <label class="bold">Tiêu đề</label>
                <input type="text" class="form-control">
            </div>
            <div class="form-group">
                <label class="bold">Mô tả ngắn</label>
                <input type="text" class="form-control">
            </div>
            <div class="form-group">
                <label class="bold">Chi tiết</label>
                <textarea class="form-control" rows="3"></textarea>
            </div>
            <div class="form-group">
                <label class="bold">Hình ảnh</label><br>
                <input type="file" name="fileUpload">
            </div>
            <div class="form-group row">
                <label class="col-lg-12 bold">Loại</label>
                <select class="form-control custom-select col-lg-2">
                    <option value="1">Thời sự</option>
                    <option value="2">Thế giới</option>
                    <option value="3">Kinh doanh</option>
                    <option value="4">Thể thao</option>
                </select>
            </div>
            <div class="form-group">
                <label class="bold">Vị trí</label><br>
                <input type="checkbox" id="vehicle1" name="vehicle1" value="">
                <label for="vehicle1">Việt Nam</label><br>
                <input type="checkbox" id="vehicle2" name="vehicle2" value="">
                <label for="vehicle2">Châu Á</label><br>
                <input type="checkbox" id="vehicle3" name="vehicle3" value="">
                <label for="vehicle3">Châu Âu</label><br>
                <input type="checkbox" id="vehicle4" name="vehicle4" value="">
                <label for="vehicle4">Châu Mỹ</label><br>
            </div>
            <div class="form-group">
                <label class="bold">Public</label><br>
                <input type="checkbox" id="" name="" value="">
                <label for="">Yes</label><br>
                <input type="checkbox" id="" name="" value="">
                <label for="">No</label><br>
            </div>
            <div class="form-group row">
                <label class="col-lg-12 bold">Date Public</label>
                <input type="date" class="form-control col-lg-3">
            </div>
            <div class="button">
                <button type="submit" class="btn btn-success">Submit</button>
                <button type="reset" class="btn btn-primary">Clear</button></button>
            </div>
        </form>
    </div>
</template>