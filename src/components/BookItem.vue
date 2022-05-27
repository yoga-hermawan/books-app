<template>
  <div class="float-left">
    <span class="float-right">
      {{ book.title }}
      <button>
        <i
          class="glyphicon glyphicon-pencil"
          @click="$emit('edit-book-item', book.id)"
          >edit</i
        >
      </button>
      <button>
        <i
          class="glyphicon glyphicon-trash"
          @click="$emit('del-book-item', book.id)"
          >delete</i
        >
      </button>
    </span>
  </div>
</template>

<script>
export default {
  name: "BookItem",
  props: ["book"],
};
</script>