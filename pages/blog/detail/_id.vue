<template>
  <div>
    <h1>Thông tin hiển thị</h1>
    <table class="table table-bordered">
      <thead>
      <tr>
        <th scope="col">id</th>
        <th scope="col">Name</th>
        <th scope="col">author</th>
      </tr>
      </thead>
      <tbody>
      <tr>
        <th scope="row">1</th>
        <td>{{blog.name}}</td>
        <td>{{blog.author}}</td>
        <td>
          <button class="btn btn-dark" @click="$router.push('/blog')">back</button>
        </td>
      </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
    export default {
        mounted() {
            this.getData()
        },
        data() {
            return {
                blog: {
                    name: '',
                    author: ''
                }
            }
        },
        methods: {
            getData() {
                let self = this;
                this.$axios.get('http://127.0.0.1:4000/blog/' + this.$route.params.id)
                    .then(function (res) {
                        self.blog = res.data.data
                    })
            },
        }

    }
</script>
