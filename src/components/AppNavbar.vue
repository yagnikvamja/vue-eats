<script setup>
import { useCurrentUser, useFirebaseAuth } from 'vuefire'
import { signOut } from 'firebase/auth'

const user = useCurrentUser()
console.log('user :>> ', user)

const auth = useFirebaseAuth()

async function signOutFromFirebase() {
  signOut(auth)
    .then(() => {
      console.log('Sign-out successful')
    })
    .catch((error) => {
      console.error('Sign-out error', error)
    })
}
</script>

<template>
  <v-app-bar color="teal">
    <v-app-bar-title>Vue Eats</v-app-bar-title>
    <v-spacer></v-spacer>
    <nav class="pr-4">
      <v-btn to="/">Home</v-btn>
      <v-btn to="/new">New</v-btn>
      <v-btn v-if="user" @click="signOutFromFirebase">Sign-Out</v-btn>
      <v-btn v-else to="/sign-in">Sign-In</v-btn>
    </nav>
  </v-app-bar>
</template>

<style></style>
