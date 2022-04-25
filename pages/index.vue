<template>
  <p>{{ message }}</p>
</template>

<script>
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
