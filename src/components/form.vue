<template>
  <form @submit.prevent="handleAddTask">
    <h1 class="title">
      Hi {{ username.split(" ")[0] }}. What are your ToDos for today?
      <time class="date date--dark">
        {{ `${date[0]}, ${date[1]} ${date[2]} ${date[3]}` }}
      </time>
    </h1>

    <div class="form-input-group">
      <label aria-label="new-task">
        <input
          autoFocus
          required
          type="text"
          maxLength="100"
          :name="username"
          v-model="this.newTask"
          aria-label="username"
          placeholder="e.g Update Wordpress ..."
        />
      </label>
      <button aria-roledescription="form submission">Enter</button>
    </div>
  </form>
</template>

<script>
export default {
  name: "form-component",
  props: {
    username: {
      type: String,
      required: true,
      default: "",
    },
  },
  data() {
    return {
      newTask: null,
      lastId: 0,
      date: new Date(Date.now()).toString().split(" "),
    };
  },

  watch: {
    lastId(oldLastId) {
      localStorage.setItem("lastId", oldLastId);
    },
  },

  created() {
    this.lastId = parseInt(localStorage.getItem("lastId") || 0);
  },

  methods: {
    handleAddTask(event) {
      event.preventDefault();
      console.log("called");
      this.$emit("setTasks", {
        completed: false,
        title: this.newTask,
        id: this.lastId + 1,
      });

      this.newTask = "";
      this.lastId = this.lastId + 1;
    },
  },
};
</script>
