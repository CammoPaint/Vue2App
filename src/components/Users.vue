<template>
  <div class="users">
    <h1>{{ name }}</h1>
    <div class="panel panel-default" v-for="user of users" :key="user.id">
      <div class="panel-heading">{{user.username}}</div>
      <div class="panel-body">
          <strong>{{user.name}}</strong>
          <p>{{user.address.street}}<br/>
          {{user.address.suite}}<br/>
          {{user.address.zipcode}}</p>
      </div>
    </div>
</div>
</template>

<script>
import UserService from '../services/UserService'

export default {
  data () {
    return {
      name: 'Users',
      users: [],
      errors: []
    }
  },
  created: function () {
    UserService.get((data) => {
      this.users = data
    }, (response) => {
      this.errors.push(response.errors)
    })
  }
}
</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>