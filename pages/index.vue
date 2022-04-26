<template>
  <p>{{ message }}</p>
</template>

<script>
const axios = require("axios").default;
export default {
  data() {
    return {
      message: "",
    };
  },
  computed: {
    test() {
      return this.$auth.strategy.token.get();
    },
  },
  mounted() {
    if (!this.$auth.loggedIn) {
      this.$router.push("auth/login");
    }
    const id = this.$auth.user._id;
    console.log(this.$auth);
    try {
      this.$axios
        .$get(`/users/${id}`, {
          headers: {
            "Content-Type": "application/json",
            "auth-token": this.test.split(" ")[1],
          },
        })
        .then((response) => {
          console.log(response);
          this.message = "Hi " + response.email;
          this.$nuxt.$emit("auth", true);
        });
    } catch (e) {
      this.message = "You are not logged in";
      this.$nuxt.$emit("auth", false);
    }
  },
};
</script>
