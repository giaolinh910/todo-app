<template class="all">
   <div class="container" style="max-width: 600px">
    <h2 class="text-center mt-5">Todo App</h2>

    <div class="d-flex mt-5">
      <input
        type="text"
        v-model="task"
        placeholder="Nhập công việc"
        class="w-100 form-control"
      />
      <button class="btn btn-warning rounded-0" @click="submitTask">
        SUBMIT
      </button>
    </div>

    <table class="table table-bordered mt-5">
      <thead>
        <tr>
          <th scope="col">Công việc</th>
          <th scope="col">Trạng thái</th>
          <th scope="col" class="text-center">Xóa</th>
          <th scope="col" class="text-center">Sửa</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(task, index) in tasks" :key="index">
          <td>
            <span :class="{ 'line-through': task.status === 'finished' }">
              {{ task.name }}
            </span>
          </td>
          <td>
            <span
              class="pointer noselect"
              @click="changeStatus(index)"
              :class="{
                'text-danger': task.status === 'Việc cần làm',
                'text-success': task.status === 'Đang làm',
                'text-warning': task.status === 'Đã hoàn thành',
              }"
            >
              {{ capitalizeFirstChar(task.status) }}
            </span>
          </td>
          <td class="text-center">
            <div @click="deleteTask(index)">
              <span class="fa fa-trash pointer"></span>
            </div>
          </td>
          <td class="text-center">
            <div @click="editTask(index)">
              <p class="fa fa-pen pointer"></p>
            </div>
          </td>
        </tr>
      </tbody>
    </table>

  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data() {
    return {
      task: "",
      editedTask: null,
      statuses: ["Việc cần làm", "Đang làm", "Đã hoàn thành"],
      tasks: [
        {
          name: "Ăn cơm đúng giờ",
          status: "Việc cần làm",
        },
        {
          name: "Chạy bộ 30p ",
          status: "Việc cần làm",
        },
        {
          name: "Đọc sách 30p",
          status: "Việc cần làm",
        },
      ],
    };
  },

  methods: {
    capitalizeFirstChar(str) {
      return str.charAt(0).toUpperCase() + str.slice(1);
    },
    changeStatus(index) {
      let newIndex = this.statuses.indexOf(this.tasks[index].status);
      if (++newIndex > 2) newIndex = 0;
      this.tasks[index].status = this.statuses[newIndex];
    },
    deleteTask(index) {
      this.tasks.splice(index, 1);
    },
    editTask(index) {
      this.task = this.tasks[index].name;
      this.editedTask = index;
    },
    submitTask() {
      if (this.task.length === 0) return;
      if (this.editedTask != null) {
        this.tasks[this.editedTask].name = this.task;
        this.editedTask = null;
      } else {
        this.tasks.push({
          name: this.task,
          status: "Việc cần làm",
        });
      }

      this.task = "";
    },
  },
   
}
</script>
<style scoped>
  .pointer {
  cursor: pointer;
}
.noselect {
  -webkit-touch-callout: none; 
  -webkit-user-select: none; 
  -khtml-user-select: none; 
  -moz-user-select: none; 
  -ms-user-select: none; 
  user-select: none; 
}
.line-through {
  text-decoration: line-through;
}
</style>>

