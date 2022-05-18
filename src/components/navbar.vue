<template>
  <nav>
    <span className="logo">Matin Nikookar | Vue</span>
    <div>
      <label>
        <input
          readOnly
          maxLength="15"
          aria-label="username"
          type="text"
          placeholder="Your Username ..."
          :value="username"
        />
      </label>
    </div>
  </nav>
</template>

<script>
export default {
  name: "nav-bar",
  props: {
    username: {
      type: String,
      required: true,
      default: "",
    },
  },
};
</script>
