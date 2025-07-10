<template>
  <div class="login-container">
    <h2>Login</h2>
    <Alert v-if="alert.show" :type="alert.type" :message="alert.message" @close="alert.show = false" />
    <input v-model="username" placeholder="Username" class="login-input" />
    <input v-model="password" type="password" placeholder="Password" class="login-input" />
    <button @click="login" class="login-button">Login</button>
    <p v-if="error" style="color:red">{{ error }}</p>
    <router-link to="/register" class="register-link">Belum punya akun? Daftar di sini</router-link>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import { useRouter } from 'vue-router'
import { auth } from '../store/auth'
import Alert from '../components/Alert.vue'

const username = ref('')
const password = ref('')
const router = useRouter()
const error = ref('')
const alert = ref({ show: false, type: '', message: '' })

function showAlert(type, message) {
  alert.value = { show: true, type, message }
  setTimeout(() => { alert.value.show = false }, 2500)
}

async function login() {
  error.value = ''
  const ok = await auth.login(username.value, password.value)
  if (ok) {
    showAlert('success', 'Login berhasil!')
    setTimeout(() => {
      if (auth.role === 'admin') router.push('/admin')
      else router.push('/uts')
    }, 1200)
  } else {
    error.value = 'Login gagal, cek username/password.'
  }
}
</script>

<style scoped>
.login-container {
  max-width: 360px;
  margin: 5rem auto;
  padding: 2rem;
  background: #FFEBEE; 
  border-radius: 12px;
  box-shadow: 0 8px 16px rgba(0,0,0,0.1); 
  text-align: center;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  color: #424242; 
}

.login-container h2 {
  margin-bottom: 1.5rem;
  color: #880E4F; 
  font-weight: 700;
  font-size: 2rem;
}

.login-input {
  width: calc(90% - 4px);
  padding: 0.75rem 1rem;
  margin-bottom: 1rem;
  border: 2px solid #F48FB1; 
  border-radius: 8px;
  font-size: 1.1rem;
  outline: none;
  transition: border-color 0.3s ease;
  color: #424242; 
}

.login-input:focus {
  border-color: #EC407A; 
  box-shadow: 0 0 8px rgba(236, 64, 122, 0.5); 
}

.login-button {
  width: 100%;
  padding: 0.75rem 1rem;
  background-color: #EC407A; 
  color: white; 
  font-size: 1.1rem;
  font-weight: 700;
  border: none;
  border-radius: 8px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.login-button:hover {
  background-color: #D81B60; 
}

.register-link {
  display: block;
  margin-top: 1.5rem;
  color: #EC407A; 
  font-weight: 500;
  text-decoration: underline;
  cursor: pointer;
}

.register-link:hover {
  color: #D81B60; 
}

.login-container p[style="color:red"] {
  color: #DC143C !important;
}
</style>