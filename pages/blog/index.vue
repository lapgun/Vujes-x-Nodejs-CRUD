<template>
  <div>
    <button class="btn btn-success" @click="$router.push('/blog/create')" >Create User</button>

    <input type="text" v-model="search">
    <button class="btn btn-success" @click="getBlogs" >Search</button>
    <table class="table table-bordered">
      <thead>
      <tr>
        <th>id</th>
        <th>blog name</th>
        <th>author</th>
        <th></th>
      </tr>
      </thead>
      <tbody>
      <tr v-for="(blog,index) in blogs" >
        <td>{{index ++}}</td>
        <td>{{blog.name}}</td>
        <td>{{blog.author}}</td>
        <td>
          <button class="btn btn-info" @click="$router.push('/blog/edit/'+ blog.id)" >Edit</button>
          <button class="btn btn-danger" @click="deleteBlog(blog.id)">Delete</button>
          <button class="btn btn-secondary" @click="$router.push('/blog/detail/'+blog.id)">Detail</button>
        </td>
      </tr>
      </tbody>
    </table>
  </div>
</template>


<script>
    export default {
        mounted(){
            this.getBlogs()
        },
        data() {
            return{
                blogs : {},
                search:''
            }
        },
        methods : {
            getBlogs(){
                let self = this;
                this.$axios.get('http://127.0.0.1:4000/blogs?search='+ this.search)
                    .then(function (res) {
                        self.blogs =res.data.data
                    });
                this.search = ''
            },
            deleteBlog(id){
                let self = this;
                this.$axios.delete('http://127.0.0.1:4000/blog/'+id)
                    .then(function (res) {
                        self.getBlogs();
                    })
            }
        }
    }
</script>

<style scoped>

</style>
