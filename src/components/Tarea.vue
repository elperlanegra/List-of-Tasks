<template>
  <div>
    <h1 class="display-4 text-center">List of Tasks</h1>
    <hr />
    <div class="row">
      <div class="col-lg-8 offset-lg-2">
        <div class="card mt-4">
          <div class="card-body">
            <div class="input-group">
              <input
                type="text"
                v-model="task"
                class="form-control form-control-lg"
                placeholder="add task"
              />

              <div class="input-group-append">
                <button v-on:click="addTask()" class="btn btn-success btn-lg">
                  <span>
                    <i class="fas fa-plus-circle"></i>
                  </span>
                  Add Task
                </button>
              </div>
            </div>

            <br />

            <div>
              <h5 v-if="listTareas.length == 0">
                <span>
                  <i class="fas fa-tasks"></i>
                  No hay tareas para realizar
                </span>
              </h5>
              <h5 v-else-if="listTareas.length">
                <span>
                  <i class="fas fa-tasks"></i>
                  Task
                </span>
              </h5>
            </div>

            <ul class="list-group">
              <li
                v-for="(task, index) of listTareas"
                :key="index"
                class="list-group-item d-flex bd-highlight mb-3"
              >
                <div class="p-2 bd-highlight">
                  <span
                    v-bind:class="{ 'text-success' : task.status  }"
                    v-on:click="editTask(task, index)" class="cursor">
                    <i
                      v-bind:class="[
                        task.status ? 'fas fa-check-circle' : 'far fa-circle',
                      ]"
                    ></i>
                  </span>

                  {{ task.name }}
                </div>

                <div class="ms-auto p-2 bd-highlight">
                  <span
                    v-on:click="removeTask(index)"
                    class="text-danger cursor"
                  >
                    <i class="fas fa-trash"></i>
                  </span>
                </div>
              </li>
            </ul>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Tarea",

  data() {
    return {
      task: "",
      listTareas: [],
    };
  },

  methods: {
    addTask() {
      const task = {
        name: this.task,
        status: false,
      };
      this.listTareas.push(task);
      this.task = "";
    },

    removeTask(index) {
      this.listTareas.splice(index, 1);
    },

    editTask(task, index) {
      this.listTareas[index].status = !task.status;
    },
  },
};
</script>

<style lang="css" scoped>
.cursor {
  cursor: pointer;
}
</style>