<script setup lang="ts">
import { onMounted } from "vue";
import liff from "@line/liff";
defineProps<{ msg: string }>();

onMounted(() => {
  console.log("init");
  liff.init({ liffId: "1657157290-r55nwMOv" }, () => {
    if (liff.isLoggedIn()) {
      runApp();
    } else {
      liff.login();
    }
  });
});
function runApp() {
  const idToken = liff.getIDToken();
  console.log(idToken);
  liff.permission.query("email").then((permissionStatus) => {
    // permissionStatus = { state: 'granted' }
    console.log(permissionStatus);
  });
  // liff
  //   .getProfile()
  //   .then((profile) => {
  //     console.log(profile);
  //   })
  //   .catch((err) => console.error(err));
}
</script>

<template>
  <h1>{{ msg }}</h1>

  <p>
    Recommended IDE setup:
    <a href="https://code.visualstudio.com/" target="_blank">VS Code</a>
    +
    <a href="https://github.com/johnsoncodehk/volar" target="_blank">Volar</a>
  </p>

  <p>See <code>README.md</code> for more information.</p>

  <p>
    <a href="https://vitejs.dev/guide/features.html" target="_blank">
      Vite Docs
    </a>
    |
    <a href="https://v3.vuejs.org/" target="_blank">Vue 3 Docs</a>
  </p>

  <button type="button">count is: a</button>
  <p>
    Edit
    <code>components/HelloWorld.vue</code> to test hot module replacement.
  </p>
</template>

<style scoped>
a {
  color: #42b983;
}

label {
  margin: 0 0.5em;
  font-weight: bold;
}

code {
  background-color: #eee;
  padding: 2px 4px;
  border-radius: 4px;
  color: #304455;
}
</style>
