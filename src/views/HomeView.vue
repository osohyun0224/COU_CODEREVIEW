<template>
  <div id="app">
    <div class="editor">
      <div class="line" v-for="(line, index) in lines" :key="index">
        <span class="line-number">{{ index + 1 }}</span>
        <div class="line-content" 
             contenteditable="true" 
             @input="updateLine($event.target.innerText, index)" 
             @keydown.enter.prevent="addLine(index)" 
             @focus="selectedLine = index" 
             @blur="selectedLine = null"
             :class="{ 'line-selected': index === selectedLine }"></div>
      </div>
    </div>
    <button @click="submitCode">코드 제출</button>
    <pre>{{ submittedCode }}</pre>
  </div>
</template>

<script>
export default {
  data() {
    return {
      lines: [''],
      submittedCode: '',
      selectedLine: null
    };
  },
  methods: {
    addLine(index) {
      this.lines.splice(index + 1, 0, '');
      this.$nextTick(() => {
        this.$el.querySelectorAll('.line-content')[index + 1].focus();
      });
    },
    updateLine(text, index) {
      this.lines.splice(index, 1, text);
    },
    submitCode() {
      this.submittedCode = this.lines.join('\n');
    }
  }
}
</script>

<style>
.editor {
  width: 500px;
  height: 300px;
  background-color: #282828;
  padding: 10px;
  overflow: auto;
}

.line {
  display: flex;
  margin-bottom: 10px;
}

.line-number {
  color: #999;
  margin-right: 10px;
}

.line-content {
  color: #F8F8F2;
  background-color: #282828;
  border: none;
  flex-grow: 1;
  min-height: 18px;
}

.line-content:focus {
  outline: none;
}

.line-content.line-selected {
  background-color: #444;
}
</style>
