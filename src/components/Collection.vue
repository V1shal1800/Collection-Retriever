<template>
  <div :class="'container1'">
    <h3>
      {{ collection.name }}
    </h3>
    <p>created At: {{ new Date(collection.createdAt).toLocaleString() }}</p>
  </div>
</template>

<script>
export default {
  name: 'Collection',
  props: {
    collection: Object,
  },
}
</script>

<style scope>
.container1 {
  background: #f4f4f4;
  margin: 5px;
  padding: 10px 20px;
 }
.container1.new {
  border-left: 5px solid green;
}  
.container1 h3 {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
</style>