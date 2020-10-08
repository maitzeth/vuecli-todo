<template>
  <div>
    <form @submit.prevent="handleSubmit">
      <input type="text" name="title" placeholder="Title..." v-model="title" />
      <button type="submit" class="btn">Submit</button>
    </form>
  </div>
</template>

<script>
export default {
  name: "AddForm",
  data() {
    return {
      title: "",
    };
  },
  methods: {
    handleSubmit() {
      const newTodo = {
        title: this.title,
        completed: false,
      };

      this.$emit("add-todo", newTodo);

      this.title = "";
    },
  },
};
</script>

<style scoped>
form {
  display: flex;
}

input[type="text"] {
  flex: 10;
}

input[type="submit"] {
  flex: 2;
}
</style>
