<template>
  <div className="intro">
    <label>
      <input
        autoFocus
        maxLength="15"
        type="text"
        aria-label="username"
        placeholder="Username. . . "
        :value="username"
        :onchange="handleChangeName"
        :onkeydown="handlePressEnter"
      />
    </label>
  </div>
</template>

<script>
export default {
  name: "login-comp",

  data() {
    return {
      username: "",
    };
  },

  methods: {
    handlePressEnter(event) {
      if (event.keyCode === 13) {
        if (this.username.length === 0)
          localStorage.setItem("username", "Guest");
        this.$emit("setLogin", false);
      }
    },
    handleChangeName(event) {
      const newName = event.target.value;
      this.username = newName;
      localStorage.setItem("username", newName);
    },
  },
};
</script>
