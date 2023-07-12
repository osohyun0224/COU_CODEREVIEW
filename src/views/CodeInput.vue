<template>
  <div class="code-input">
    <textarea v-model="code" @input="updateCode" class="code-textarea"></textarea>
    <pre>{{ code }}</pre>
  </div>
</template>

<script>
export default {
  data() {
    return {
      code: ''
    }
  },
  methods: {
    updateCode(event) {
      this.code = event.target.value;
    }
  }
}
</script>

<style scoped>
.code-input {
  margin: 0 auto;
  width: 80%;
}

.code-textarea {
  width: 100%;
  height: 200px;
  margin-bottom: 10px;
}
</style>