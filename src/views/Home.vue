<template>
  <div class="wrapper">
    <!-- Components -->
    <textarea :value="input" @input="update"></textarea>
    <div v-html="compiledMarkdown"></div>
  </div>
</template>

<script>
import marked from "vue-marked";

export default {
  computed: {
    compiledMarkdown() {
      return marked(this.input, { sanitize: true });
    }
  },
  components: {},
  data: () => {
    input: "# Hello World!";
  },
  methods: {
    update: _.debounce(function(e) {
      this.input = e.target.value;
    }, 300)
  }
};
</script>

<style lang="scss">
.wrapper {
  width: 100%;
  height: 100%;
  display: flex;
  justify-content: center;

  textarea,
  div {
    display: inline-block;
    width: 49%;
    height: 100%;
    vertical-align: top;
    box-sizing: border-box;
    padding: 0 20px;
  }

  textarea {
    border: none;
    border-right: 1px solid #ccc;
    resize: none;
    outline: none;
    background-color: #f6f6f6;
    font-size: 14px;
    font-family: "Monaco", courier, monospace;
    padding: 20px;
  }

  code {
    color: #f66;
  }
}
</style>
