<template>
  <Login v-if="login" @setLogin="setLogin" />

  <div class="app app--dark">
    <Navbar :username="username" />

    <section>
      <Form @setTasks="setTasks" :username="username" />

      <div className="task-group">
        <span className="task-group-title">
          Open Tasks
          <small> ({{ tasks?.length - completedCount }})</small>
        </span>
        <template v-for="task in tasks">
          <TaskItem
            v-if="!task.completed"
            :completed="false"
            @onDelete="() => handleDeleteTask(task.id)"
            @onChangeTaskStatus="
              (id, status) => handleChangeTaskStatus(task.id, status)
            "
            :key="task"
            :title="task.title"
          />
        </template>
      </div>

      <div className="task-group">
        <span className="task-group-title">
          Finished Tasks
          <small> ({{ completedCount }})</small>
        </span>
        <template v-for="task in tasks">
          <TaskItem
            v-if="task.completed"
            :completed="true"
            @onDelete="() => handleDeleteTask(task.id)"
            @onChangeTaskStatus="
              (id, status) => handleChangeTaskStatus(task.id, status)
            "
            :key="task"
            :title="task.title"
          />
        </template>
      </div>
    </section>
  </div>
</template>

<script>
import TaskItem from "./components/taskItem.vue";
import Navbar from "./components/navbar.vue";
import Login from "./components/login.vue";
import Form from "./components/form.vue";

export default {
  name: "App",

  components: {
    Navbar,
    TaskItem,
    Form,
    Login,
  },

  data() {
    return {
      login: false,
      username: "Matin",
      completedCount: 0,
      tasks: [],
    };
  },

  watch: {
    login(oldLogin) {
      if (oldLogin !== true)
        setTimeout(() => {
          this.username = localStorage.getItem("username")
            ? localStorage.getItem("username")
            : "User";
        }, 3600);
    },
    tasks(oldTasks) {
      localStorage.setItem("tasks", JSON.stringify(oldTasks));
      let completedCount = 0;
      oldTasks?.map((task) => {
        if (task.completed) completedCount++;
        return task;
      });
      this.completedCount = completedCount;
    },
  },

  created() {
    const cachedTasks = JSON.parse(localStorage.getItem("tasks"));
    this.tasks =
      cachedTasks === null ? [] : JSON.parse(localStorage.getItem("tasks"));
    this.login = localStorage.getItem("username") ? false : true;
  },

  methods: {
    setLogin(val) {
      this.login = val;
    },

    setTasks(vals) {
      this.tasks = [...this.tasks, { ...vals }];
    },

    handleDeleteTask(id) {
      console.log(id);
      const tempState = [...this.tasks];
      const taskToRemoveIndex = tempState.findIndex((item) => item.id === id);
      tempState.splice(taskToRemoveIndex, 1);
      this.tasks = [...tempState];
    },

    handleChangeTaskStatus(id, status) {
      console.log(id, status);
      const tempState = [...this.tasks];
      const taskToModifyIndex = tempState.findIndex((item) => item.id === id);
      const taskToModify = tempState.splice(taskToModifyIndex, 1);
      taskToModify[0].completed = status;
      tempState.push(taskToModify[0]);
      this.tasks = [...tempState];
    },
  },
};
</script>

<style lang="scss">
@import "./stylesheets/main.scss";
</style>
