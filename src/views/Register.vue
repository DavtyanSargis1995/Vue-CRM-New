<template>
    <form class="card auth-card" @submit.prevent="submitHandler">
        <div class="card-content">
          <span class="card-title">Домашняя бухгалтерия</span>
          <div class="input-field">
            <input
              id="email"
              type="text"
              class="validate"
              v-model.trim="email"
              :class = "{invalid: ($v.email.$dirty && (!$v.email.required || !$v.email.email))}"
            >
            <label for="email">Email</label>
            <small
              class="helper-text invalid"
              v-if = "$v.email.$dirty && !$v.email.required"
            >
              The email is required
            </small>
            <small
              class="helper-text invalid"
              v-else-if="$v.email.$dirty && !$v.email.email"
            >
              Wrong email format
            </small>
          </div>
          <div class="input-field">
            <input
              id="password"
              type="password"
              class="validate"
              v-model.trim="password"
              :class = "{invalid: ($v.password.$dirty && (!$v.password.required || !$v.password.minLength))}"
            >
            <label for="password">Пароль</label>
            <small
              class="helper-text invalid"
              v-if = "$v.password.$dirty && !$v.password.required"
            >
              The password is required
            </small>
            <small
              class="helper-text invalid"
              v-else-if="$v.password.$dirty && !$v.password.minLength"
            >
              The password minimum length is {{$v.password.$params.minLength.min}} characters. Now it's {{password.length}}
            </small>
          </div>
          <div class="input-field">
              <input
                    id="name"
                    type="text"
                    class="validate"
                    v-model.trim="name"
              >
              <label for="name">Имя</label>
            <small
              class="helper-text invalid"
              v-if = "$v.name.$dirty && !$v.name.required"
            >
              The name is required
            </small>
          </div>
          <p>
              <label>
                  <input type="checkbox" v-model="agree"/>
                  <span>С правилами согласен</span>
              </label>
          </p>
        </div>
        <div class="card-action">
            <div>
                <button
                        class="btn waves-effect waves-light auth-submit"
                        type="submit"
                >
                    Зарегистрироваться
                    <i class="material-icons right">send</i>
                </button>
            </div>

            <p class="center">
                Уже есть аккаунт?
                <router-link to="/">Войти!</router-link>
            </p>
        </div>
    </form>
</template>

<script>
import { email, minLength, required } from 'vuelidate/lib/validators'
export default {
  name: 'register',
  data: () => ({
    email: '',
    password: '',
    name: '',
    agree: false
  }),
  methods: {
    submitHandler () {
      if (this.$v.$invalid) {
        this.$v.$touch()
        return
      }
      const formData = {
        email: this.email,
        password: this.password,
        name: name
      }
      console.log(formData)
      this.$router.push('/')
    }
  },
  validations: {
    email: { email, required },
    password: { required, minLength: minLength(12) },
    name: { required },
    agree: { checked: v => v }
  }
}
</script>
