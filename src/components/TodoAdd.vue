<template>
  <div>
    <label for="content">New Todo</label>
    <div class="form-group">
      <input type="text" class="content" v-model="item.name" />
      <button class="btn-add" @click="add">Add</button>
    </div>
    <div class="error" v-if="showErrors">Content cannot be empty</div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      item: {
        name: "",
        isDone: false,
        showFormTodo: false,
      },
      showErrors: false,
    };
  },
  methods: {
    add() {
      if (this.item.name == "") {
        this.showErrors = true;
      } else {
        this.showErrors = false;
        this.$emit("items", this.item);
        this.item = {
          name: "",
          isDone: false,
          showFormTodo: false,
        };
      }
    },
  },
};
</script>
