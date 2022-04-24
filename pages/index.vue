<template>
  <p>{{ message }}</p>
</template>

<script lang="ts">
import Vue from "vue";
export default Vue.extend({
  data() {
    return {
      message: "",
    };
  },
  async mounted() {
    try {
      const response = await fetch(`http://localhost:3000/users/${id}`, {
        headers: { "Content-Type": "application/json" },
        credentials: "include",
      });
      console.log(response);
      const content = await response.json();
      console.log(content);
      this.message = "Hi " + content.email;
      this.$nuxt.$emit("auth", true);
    } catch (e) {
      this.message = "You are not logged in";
      this.$nuxt.$emit("auth", false);
    }
  },
});
</script>
