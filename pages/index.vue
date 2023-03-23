<script setup lang="ts">
import { ofetch } from 'ofetch'
import { Buffer } from 'buffer'

// const client_id = '' // Your client id
// const client_secret = '' // Your secret
// const redirect_uri = '' // Your redirect uri
// let token: string | undefined = undefined
const config = useRuntimeConfig();

function generateRandomString (length: number) {
  var text = '';
  var possible = 'ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789';

  for (var i = 0; i < length; i++) {
    text += possible.charAt(Math.floor(Math.random() * possible.length));
  }
  return text;
}

async function login () {
  console.log('Login', config.app)
  const url = 'https://accounts.spotify.com/authorize?'

  const res = await ofetch(url, {
    method: 'GET',
    params: {
      response_type: 'code',
      client_id: config.app.spotify.clientId,
      scope: 'user-read-private user-read-email',
      redirect_uri: config.app.spotify.clientUri,
      state: generateRandomString(16),
    },
  })

  console.log(res)
}
</script>

<template>
  <div class="text-center">
    <button
      type="button"
      @click="login"
      class="spotify-btn"
    >
      Login with Spotify
    </button>
  </div>
</template>

<style scoped>
.text-center {
  text-align: center;
}

.spotify-btn {
  background-color: green;
  color: white;
  font-size: 1.8rem;
  border: none;
  border-radius: 1rem;
  padding: 0.5rem 1.6rem;
  cursor: pointer;
}

.spotify-btn:hover {
  opacity: 0.9;
}

</style>