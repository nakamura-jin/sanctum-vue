<template>
  <div class="col-5 mx-auto">
    <h1>Login</h1>
    <form>
      <div class="mb-3">
        <label for="exampleInputEmail1" class="form-label">Email</label>
        <input v-model="form.email" type="email" class="form-control" id="exampleInputEmail1" aria-describedby="emailHelp">
        <span class="text-danger" v-if="errors.email">{{ errors.email[0] }}</span>
      </div>
      <div class="mb-3">
        <label for="exampleInputPassword1" class="form-label">Password</label>
        <input v-model="form.password" type="password" class="form-control" id="exampleInputPassword1">
        <span class="text-danger" v-if="errors.password">{{ errors.password[0] }}</span>
      </div>
      <button @click.prevent="login" type="submit" class="btn btn-primary">Submit</button>
    </form>
  </div>
</template>

<script>
import User from '../apis/User'
export default {
  data() {
    return {
      form: {
        email: '',
        password: ''
      },
      errors: []
    }
  },
  methods: {
    login() {
      User.login(this.form)
      .then(() => {
        localStorage.setItem('auth', 'true')
        this.$router.push('/dashboard')
      })
      .catch(errors => {
        if(errors.response.status === 422) {
          this.errors = errors.response.data.errors
        }
      })
    }
  }
}
</script>

<style>

</style>