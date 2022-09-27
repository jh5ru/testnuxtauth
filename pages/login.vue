<template>
  <section class="section">
    <div class="container">
      <div class="columns">
        <div class="column is-4 is-offset-4">
          <h2 class="title has-text-centered">Welcome back!</h2>

          <Notification :message="error" v-if="error"/>

          <form method="post" @submit.prevent="login">
            <div class="field">
              <label class="label">Email</label>
              <div class="control">
                <input
                  type="email"
                  class="input"
                  name="email"
                  v-model="email"
                />
              </div>
            </div>
            <div class="field">
              <label class="label">Password</label>
              <div class="control">
                <input
                  type="password"
                  class="input"
                  name="password"
                  v-model="password"
                />
              </div>
            </div>
            <div class="control">
              <button type="submit" class="button is-dark is-fullwidth">Log In</button>
            </div>
          </form>
          <div class="has-text-centered" style="margin-top: 20px">
            <p>
              Don't have an account? <nuxt-link to="/register">Register</nuxt-link>
            </p>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
import Notification from '~/components/Notification'

export default {
  components: {
    Notification,
  },

  data() {
    return {
      email: '',
      password: '',
      error: null
    }
  },

  methods: {
    async login() {
      try {
        const user = await this.$auth.loginWith('local', {
          data: {
            phone: '79500093271',
            sms_code: '4444'
          }
        }).then(({data}) => {
          console.log(data)
         // this.$axios.setToken(data.api_token, 'Bearer')
         // this.$auth.setToken('local', `Bearer ${data.api_token}`)
        });
        console.log(user)
        // await this.$store.dispatch('auths/login', { '79500093271': '4444' })

       // this.$router.push('/')
      } catch (e) {
        console.log(e)
       // this.error = e.response.data.message
      }
    }
  }
}
</script>
