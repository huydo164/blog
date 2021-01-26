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
                        <form method="get" action="">
                            <div class="form-group row">
                                <label class="col-sm-2 col-form-label">
                                    Tiêu đề
                                </label>
                                <div class="col-sm-10">
                                    <input class="form-control" placeholder="Tìm kiếm..">
                                </div>
                            </div>
                            <button class="btn btn-success">Search</button>
                        </form>
                    </div>
                    <blog-list></blog-list>
                </div>
            </div>
        </div>
    </div>
</template>
<script>
import AppMenu from '@/components/AppMenu'
import BlogList from '@/components/BlogList'
export default {
    layout: "search"
}
</script>