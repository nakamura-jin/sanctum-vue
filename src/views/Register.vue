<template>
  <div class="col-5 mx-auto">
    <h1>Register</h1>
    <form>
      <div class="mb-3">
        <label for="exampleInputName" class="form-label">Name</label>
        <input v-model="form.name" type="email" class="form-control" id="exampleInputName" aria-describedby="emailHelp">
        <span class="text-danger" v-if="errors.name">{{ errors.name[0] }}</span>
      </div>
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
      <div class="mb-3">
        <label for="exampleInputPassword_confirmation" class="form-label">Password_Confirmation</label>
        <input v-model="form.password_confirmation" type="password" class="form-control" id="exampleInputPassword_confirmation">
        <span class="text-danger" v-if="errors.password_confirmation">{{ errors.password_confirmation[0] }}</span>
      </div>
      <button @click.prevent="register" type="submit" class="btn btn-primary">Submit</button>
    </form>
  </div>
</template>

<script>
import User from '../apis/User'
export default {
  data() {
    return {
      form: {
        name: '',
        email: '',
        password: '',
        password_confirmation: '',
      },
    errors: []
    }
  },
  methods: {
    register() {
      User.register(this.form)
      .then(() => {
        this.$router.push('/login')
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