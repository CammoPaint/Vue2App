<template>
  <div class="home">
    <alert-component v-bind:alerts="alerts"></alert-component>
    <alert :alerts="alerts"></alert>
    <h1>{{ name }}</h1> 
  <div class="well">
    <form v-on:submit.prevent="onSubmit">
      <div class="form-group">
        <label for="title">Title</label>
        <input type="text" class="form-control" id="title" placeholder="Title"  v-model="post.title" name="title">
      </div>
      <div class="form-group">
          <label for="body">Body</label>
          <input type="text" class="form-control" id="body" placeholder="Body" v-model="post.body" name="body">
        </div>
      <button type="submit" class="btn btn-default">Submit</button>
    </form>
  </div>    
    <div class="panel panel-default" v-for="post of posts" :key="post.id">
      <div class="panel-heading">{{post.title}}</div>
        <div class="panel-body">
          {{post.body}}
      </div>
    </div>
  </div>
</template>

<script>
import PostService from '../services/PostService'
import Alert from '../components/Alert.vue'

export default {
  data () {
    return {
      name: 'Home',
      post: {},
      posts: [],
      errors: [],
      alerts: []
    }
  },
  created: function () {
    PostService.get((data) => {
      this.posts = data
    }, (response) => {
      this.errors.push(response.errors)
    })
  },
  methods: {
    onSubmit: function (event) {
      PostService.post(this.post, (data) => {
        // add the new item to the array
        this.posts.unshift(data)
        // clear the post item
        this.post = {}
        // show the alert
        this.alerts.push({key: new Date().getTime(), type: 'success', msg: 'New record added', title: 'Success', duration: 5000})
      }, (response) => {
        this.errors.push(response.errors)
      })
    }
  },
  components: {
    Alert
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
