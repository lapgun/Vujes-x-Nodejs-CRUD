<template>
  <div>
    <h1>Cập nhật thông tin</h1>
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
        mounted(){
            this.getUser()
        },
        data() {
            return {
                blog: {
                    name: '',
                    author: ''
                }
            }
        },
        methods:{
            getUser (){
                let self = this;
                this.$axios.get('http://127.0.0.1:4000/blog/'+ this.$route.params.id)
                    .then(function (res) {
                        self.blog = res.data.data
                    })
            },
            handelSubmit(){
                let self = this;
                this.$axios.put('http://127.0.0.1:4000/blog/' + this.blog.id , this.blog)
                    .then(function (res) {
                        self.$router.push('/blog')
                    })
            }
        }
    }
</script>

<style scoped>

</style>
