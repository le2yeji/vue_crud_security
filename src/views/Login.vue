<script setup>
import { ref } from 'vue';
import { useQuasar } from 'quasar';
import { useAuthStore } from '@/stores/useAuth';

const authStore = useAuthStore();

const $q = useQuasar();

const username = ref(null);
const password = ref(null);

const onSubmit = async () => {
  try {
    await authStore.login(username.value, password.value);
  } catch (error) {
    $q.notify({
      color: 'red-5',
      textColor: 'white',
      icon: 'warning',
      message: error
    });
  }
};
</script>

<template>
  <div class="window-height window-width row justify-center items-center">
    <q-card flat bordered class="q-pa-md" style="width: 360px">
      <q-form @submit="onSubmit" class="q-gutter-md">
        <q-card-section class="q-mb-none">
          <div class="text-h6 text-center">로그인</div>
        </q-card-section>
        <q-card-section class="q-mb-none q-gutter-y-lg">
          <q-input
            filled
            type="text"
            v-model="username"
            label="ID *"
            hint="for test: test"
            lazy-rules
            :rules="[(val) => (val && val.length > 0) || 'Please type username(ID)']"
          />
          <q-input
            filled
            type="password"
            v-model="password"
            label="Password *"
            hint="for test: test bluegreen/canary test"
            lazy-rules
            :rules="[(val) => (val !== null && val !== '') || 'Please type your password']"
          />
          <q-btn
            type="submit"
            unelevated
            color="primary"
            size="lg"
            class="full-width"
            label="Login"
            :disable="!username || !password"
          />
        </q-card-section>
      </q-form>
    </q-card>
  </div>
</template>
