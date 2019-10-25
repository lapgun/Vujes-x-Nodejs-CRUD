<template>
  <div>
    <h1>Thêm mới thông tin</h1>
    <div class="form-group">
      Blog Name:
      <input type="text" class="form-control" v-model="blog.name">
    </div>
    <div class="form-group">
      Author:
      <input type="text" class="form-control" v-model="blog.author">
    </div>
    <div>
      <button class="btn btn-primary" @click="handelSubmit">Submit</button>
    </div>
  </div>
</template>

<script>
    export default {
        data() {
            return {
                blog: {
                    name: '',
                    author: ''
                }
            }
        },
        methods: {
            handelSubmit() {
                let self = this;
                this.$axios.post('http://127.0.0.1:4000/blog', this.blog)
                    .then(function (res) {
                        // console.log(res);
                        self.$router.push('/blog')
                    })
            }
        }
    }
</script>
