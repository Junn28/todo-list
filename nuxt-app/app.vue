<script setup>
const config = useAppConfig();
const vFocus = {
  mounted: (el) => el.focus(),
};

const addTask = () => {
  const task = {
    title: config.title,
    description: config.description,
    isDone: false,
  };
  config.tasks.push(task);
  config.isCreating = !config.isCreating;
  config.title = '';
  config.description = '';
};

const deleteTask = (index) => {
  config.tasks.splice(index, 1);
};

const btnCancel = () => {
  config.isCreating = !config.isCreating;
  config.title = '';
  config.description = '';
};
</script>

<template>
  <header>
    <nav class="navbar bg-body-tertiary">
      <div class="container-fluid">
        <span class="navbar-brand mb-0 text-uppercase fw-bold fs-3">Todo List</span>
      </div>
    </nav>
  </header>

  <div class="list-task">
    <div v-if="config.tasks.length > 0" v-for="(task, index) in config.tasks" class="item-task d-flex align-items-start border-bottom pt-3 pb-4 ps-3" :key="index">
      <input type="checkbox" name="status" id="task" class="align-self-center me-2" :checked="task.isDone" v-model="task.isDone" />
      <div class="d-flex flex-column ms-2 text-capitalize">
        <div class="title-task mb-1 fw-semibold" :class="task.isDone ? 'text-decoration-line-through' : ''">
          {{ task.title }}
        </div>
        <div class="description-task small text-muted">
          {{ task.description }}
        </div>
        <a href="#" class="btn-delete mt-1" @click="deleteTask(index)">Delete</a>
      </div>
    </div>
    <p v-else class="fs-5 ms-2">Belum ada task</p>
  </div>

  <div class="action my-2">
    <button class="btn btn-primary ms-2" v-if="!config.isCreating" @click="config.isCreating = !config.isCreating">Add Task</button>
    <div class="add-card" v-else>
      <div class="card mb-2 mx-2">
        <div class="card-body p-2">
          <h5 class="card-title">Tambahkan Task</h5>
          <input v-focus v-model="config.title" class="form-control border-1" placeholder="Title" type="text" />
          <textarea v-model="config.description" class="form-control border-1 small mt-2" placeholder="Description" rows="3"></textarea>
        </div>
      </div>
      <div class="button-wrapper d-flex mx-2">
        <button class="btn btn-success me-2" @click="addTask">Save</button>
        <button class="btn btn-outline-secondary" @click="btnCancel">Cancel</button>
      </div>
    </div>
  </div>
</template>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: Arial, Helvetica, sans-serif;
}
.btn-delete {
  color: tomato;
  font-size: 14px;
}
</style>
