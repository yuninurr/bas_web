<script setup>
import router from '@/router'
import { useAuthStore } from '@/stores/auth'
import { inject, reactive } from 'vue'

const auth = useAuthStore()

const data = reactive({
  username: '',
  password: '',
  snackbar: false,
  pesanLogin: ''
})

const myAxios = inject('myAxios')

const login = () => {
  console.log('login clicked', data)

  myAxios
    .post('/auth/login', {
      username: data.username,
      password: data.password
    })
    .then(
      (res) => {
        if (res.status == 200) {
          data.pesanLogin = 'Anda Berhasil Login'
          auth.authenticated()
          router.push('about')
        }
        data.snackbar = true
      },
      (err) => {
        data.pesanLogin = 'Username atau Password Salah'
        data.snackbar = true
      }
    )
}
</script>

<template>
  <v-card class="pa-10 custom-card">
    <div>
      <v-text-field label="Username" variant="outlined" v-model="data.username"></v-text-field>
      <!-- <v-text-field type="text" v-model="data.username" /> -->
    </div>
    <div>
      <v-text-field label="Password" variant="outlined" v-model="data.password"></v-text-field>
    </div>

    <div>
      <!-- <button @click="login">Login</button> -->
      <!-- <v-btn color="blue" @click="login">Login</v-btn> -->
      <button type="login" @click="login">Login</button>
    </div>
    <v-snackbar v-model="data.snackbar">
      {{ data.pesanLogin }}
      <template v-slot:actions>
        <v-btn
          color="black"
          variant="text"
          @click="data.snackbar = false"
          style="text-transform: none"
        >
          Close
        </v-btn>
      </template>
    </v-snackbar>
  </v-card>
</template>

<style scoped>
.custom-card {
  /* background-color: transparent; */
  border-radius: 20px;
  padding: 20px;
  box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.1);
}

button {
  padding: 0.5rem 1rem;
  font-size: 1rem;
  background-color: #a7d2cb;
  color: #056676;
  border: none;
  border-radius: 10px;
  cursor: pointer;
}
</style>
