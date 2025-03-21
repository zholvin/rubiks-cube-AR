<template>
  <div id="page-frame">
    <AppHeader />
    <div class="main">
      <div id="home-content">
        <h1>Login</h1>

        <!-- 错误提示 -->
        <div v-if="error" class="alert error">{{ error }}</div>

        <!-- 登录表单 -->
        <form @submit.prevent="login">
          <div class="form-group">
            <input
                v-model="username"
                placeholder="Username"
                :class="{ 'input-error': error }"
                required
            />
          </div>
          <div class="form-group">
            <input
                v-model="password"
                type="password"
                placeholder="Password"
                :class="{ 'input-error': error }"
                required
            />
          </div>
          <button type="submit" :disabled="isSubmitting">
            {{ isSubmitting ? 'Logging in...' : 'Login' }}
          </button>
        </form>
        <p>
          Don't have an account? <router-link to="/signup">Sign up</router-link>
        </p>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import { useRouter } from 'vue-router';
import AppHeader from '@/components/headers/Header.vue';
import api from '@/utils/api';

// Reactive state
const username = ref('');
const password = ref('');
const error = ref('');
const isSubmitting = ref(false);
const router = useRouter();

// 登录函数
const login = async () => {
  isSubmitting.value = true;
  error.value = '';

  try {
    const response = await api.post('/api/login', {
      username: username.value.trim(),
      password: password.value.trim()
    });

    if (response.data.success && response.data.data.token) {
      localStorage.setItem('token', response.data.data.token);
      alert('Login successful');
      router.push('/');
    } else {
      error.value = 'Login failed, invalid response data';
    }
  } catch (err) {
    error.value = err.response?.data?.message || 'Login failed, please check your username and password';
    console.error('Login error:', err);
  } finally {
    isSubmitting.value = false;
  }
};
</script>

<style scoped>
.main {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  background: linear-gradient(227deg, #165b9c 20.72%, #81bee4 78.01%);
  border-radius: 30px;
  width: fit-content;
  margin: 2rem auto;
  padding: 20px;
  box-sizing: border-box;
}

h1 {
  font-size: clamp(40px, 5vw, 80px);
  font-family: 'Gochi Hand', cursive;
  color: #32284a;
  text-align: center;
  margin-bottom: 20px;
}

p {
  font-family: 'Baloo 2', sans-serif;
  font-size: clamp(16px, 2vw, 20px);
  color: #32284a;
  text-align: center;
  margin-top: 10px;
}

input {
  width: 100%;
  padding: 0.75rem;
  margin-bottom: 1.5rem;
  border: 1px solid #ced4da;
  border-radius: 4px;
  transition: border-color 0.3s ease;
}

.input-error {
  border-color: #dc3545;
}

button {
  width: 100%;
  padding: 0.75rem;
  background: #28a745;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  transition: background 0.3s ease;
}

button:hover:not(:disabled) {
  background: #218838;
}

button:disabled {
  background: #6c757d;
  cursor: not-allowed;
}

.alert.error {
  padding: 1rem;
  margin-bottom: 1.5rem;
  border-radius: 4px;
  background: #f8d7da;
  color: #721c24;
  border: 1px solid #f5c6cb;
  text-align: center;
  font-family: 'Baloo 2', sans-serif;
  font-size: clamp(20px, 2vw, 30px);
}

a {
  color: #007bff;
  text-decoration: none;
}

a:hover {
  text-decoration: underline;
}
</style>