<script setup>
import { ref } from 'vue'
import { useFirebaseAuth } from 'vuefire'
import { createUserWithEmailAndPassword, signInWithEmailAndPassword } from 'firebase/auth'

import BaseButton from '@/components/base/BaseButton.vue'
import BaseContainer from '@/components/base/BaseContainer.vue'
import BaseCard from '@/components/base/BaseCard.vue'
import BaseForm from '@/components/base/BaseForm.vue'
import BaseInput from '@/components/base/BaseInput.vue'
import router from '@/router'

const userInput = ref({
  email: '',
  password: '',
})

const auth = useFirebaseAuth()

async function createUser() {
  createUserWithEmailAndPassword(
    auth,
    userInput.value.email,
    userInput.value.password
  )
    .then((userCredential) => {
      // Signed up
      const user = userCredential.user
      console.log('user :>> ', user);
      router.push('/')
    })
    .catch((error) => {
      const errorCode = error.code
      const errorMessage = error.message
      // ..
    })
}

async function SignInToFirebase() {
  signInWithEmailAndPassword(
    auth,
    userInput.value.email,
    userInput.value.password
  )
    .then((userCredential) => {
      // Signed up
      const user = userCredential.user
      console.log('user :>> ', user);
      router.push('/')
    })
    .catch((error) => {
      const errorCode = error.code
      const errorMessage = error.message
      // ..
    })
}
</script>

<template>
  <BaseContainer>
    <h1 class="mb-4">Sign In</h1>
    <BaseCard>
      <template v-slot:default>
        <BaseForm>
          <BaseInput
            v-model="userInput.email"
            type="email"
            label="Email"
            required
            placeholder="eleanorshellstrop@thegoodplace.com"
          />
          <BaseInput
            v-model="userInput.password"
            label="Password"
            type="password"
            required
          />
        </BaseForm>
      </template>
      <template v-slot:actions>
        <BaseButton variant="tonal" color="success" @click="SignInToFirebase"> Sign In </BaseButton>
        <BaseButton
          @click="createUser"
          variant="tonal"
          color="secondary"
          outline
        >
          Create New User
        </BaseButton>
      </template>
    </BaseCard>
  </BaseContainer>
</template>

<style></style>
