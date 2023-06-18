<template>
  <div class="code-input" :class="{ dark: darkMode }">
    <div class="line-numbers">
      <span v-for="(line, index) in codeLines" :key="index">{{ index + 1 }}</span>
    </div>
    <div class="code-area-wrapper">
      <textarea class="code-area" v-model="code" rows="50" cols="200" @input="updateCodeLines"></textarea>
      <div class="code-markers">
        <div class="marker" v-for="(line, index) in codeLines" :key="index" :style="markerStyle(index)"></div>
      </div>
    </div>
    <div class="code-lines"></div>
  </div>
  <button @click="addLine">줄 추가하기</button>
  <button @click="runCode">코드 실행하기</button>
  <button @click="toggleDarkMode">다크모드</button>

  <h2>댓글 작성</h2>
  <form @submit.prevent="addComment">
  <div class="comment-input">
    <label for="name">이름:</label>
    <input type="text" id="name" v-model="newComment.name" required>
  </div>
  <div class="comment-input">
    <label for="content">댓글 내용:</label>
    <textarea id="content" v-model="newComment.content" required></textarea>
  </div>
  <button type="submit">댓글 작성</button>
</form>
  <hr>
  <h3>댓글 목록</h3>
  <ul>
    <li v-for="comment in comments" :key="comment.id">
      <strong>{{ comment.name }}</strong>: {{ comment.content }}
    </li>
  </ul>
</template>

<script>
export default {
  data() {
    return {
      code: '',
      codeLines: [],
      darkMode: false,
      newComment: {
        name: '',
        content: ''
      },
      comments: []
    };
  },
  methods: {
    addLine() {
      this.code += '\n';
      this.updateCodeLines();
    },
    runCode() {
      alert(this.code);
    },
    toggleDarkMode() {
      this.darkMode = !this.darkMode;
    },
    updateCodeLines() {
      this.codeLines = this.code.split('\n');
    },
    markerStyle(index) {
      const lineHeight = 1.5; // Adjust this value to match the line height in pixels
      
      return {
        top: `${(index + 1) * lineHeight}em`,
      };
    },
    addComment() {
      // 새로운 댓글을 댓글 목록에 추가
      this.comments.push({
        id: this.comments.length + 1,
        name: this.newComment.name,
        content: this.newComment.content
      });

      // 입력 필드 초기화
      this.newComment.name = '';
      this.newComment.content = '';
    }
  }
};
</script>
<style>
.code-input {
  position: relative;
  display: flex;
}

.dark .code-area {
  background-color: #272727;
  color: #fff;
}

.line-numbers {
  width: 2em;
  padding: 8px;
  font-family: monospace;
  font-size: 14px;
  text-align: right;
  pointer-events: none;
}

.line-numbers span {
  display: block;
  border-bottom: 1px dotted #ccc;
  height: 1.5em;
  line-height: 1.5em;
}

.code-area-wrapper {
  position: relative;
  flex-grow: 1;
  margin-left: 10px;
  transition: background-color 0.3s ease, color 0.3s ease;
}

.code-area {
  width: 100%;
  font-family: monospace;
  font-size: 20px; /* 수정된 부분 */
  transition: background-color 0.3s ease, color 0.3s ease;
}

.code-markers {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  pointer-events: none;
}

.marker {
  position: absolute;
  bottom: 0;
  left: 0;
  width: 100%;
  border-bottom: 1px dotted #ccc;
  pointer-events: none;
}

.code-lines {
  flex-grow: 1;
}

.code-lines:before {
  content: "";
  display: block;
  position: absolute;
  top: 0;
  right: 100%;
  width: 2em;
  border-left: 1px dotted #ccc;
  height: 100%;
}
.comment-input {
  display: flex;
  align-items: center;
  margin-bottom: 10px;
}

.comment-input label {
  margin-right: 10px;
}
button {
  margin: 24px 0;
  max-width: 400px;
  padding: 8px 16px;
  border-radius: 24px;
  font-size: 14pt;
  color: white;
  background-color: #ca434c;
}
#name {
    padding: 8px 12px;
    margin-top: 18px;
    border: 1px solid gray;
    border-radius: 46.25px;
    background-color: #f1f1f1;
    display: flex;
    align-items: center;
    width: 300px;
    opacity: 0.7;
}
#content {
    padding: 8px 12px;
    margin-top: 18px;
    border: 1px solid gray;
    border-radius: 20px;
    background-color: #f1f1f1;
    display: flex;
    align-items: center;
    width: 800px;
    height: 400px;
    opacity: 0.7;
  }


</style>