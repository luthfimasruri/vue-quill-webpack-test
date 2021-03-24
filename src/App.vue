<template>
  <input-rich-text v-model="myEditorContent" />
  <h2>This is my editor content</h2>
  <pre>
    <code>{{ myEditorContent }}</code>
  </pre>
</template>

<script>
import { ref } from "vue";
import InputRichText from "./components/InputRichText.vue";

export default {
  name: "App",
  components: {
    InputRichText,
  },
  setup: () => {
    return {
      myEditorContent: ref("My Initial Content...."),
    };
  },
};
</script>
