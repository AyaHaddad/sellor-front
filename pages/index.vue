<template>
  <p>{{ message }}</p>
</template>

<script>
const axios = require('axios').default;
export default {
  data() {
    return {
      message: "",
    };
  },
  mounted() {
    const id = "666633333";
    console.log(this.$auth);
    try {

      // Axios test
      axios({
        method: 'get',
        url: 'http://localhost:3000/products',
        headers: {
          'Content-Type': 'application/json',
          'auth-token': 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJfaWQiOiI2MjU0NDNiYTM5ZWJjYzA0M2EwN2UzMDgiLCJpYXQiOjE2NDk2ODk1MzV9.P0t6d8gWp0ze8Xn1KZ_CDx_TFJzEL37LtGlSqmT9mQQ'
        }
      }).then(function (res) {console.log(res);});
      // End of Axios test

      fetch(`http://localhost:3000/users/${id}`, {
        headers: {
          "Content-Type": "application/json",
          "auth-token": "",
        },
        credentials: "include",
      }).then((response) => {
        console.log(response);
        const content = response.json();
        console.log(content);
        this.message = "Hi " + content.email;
        this.$nuxt.$emit("auth", true);
      });
    } catch (e) {
      this.message = "You are not logged in";
      this.$nuxt.$emit("auth", false);
    }
  },
};
</script>
