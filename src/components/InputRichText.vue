<template>
  <div
    class="form-field"
    :class="[
      {
        'not-empty': modelValue?.toString().length > 0,
        'form-field--disabled': disabled,
        'form-field--requesting': requesting,
        'form-field--success': success,
        'form-field--error': typeof error === 'string' && error?.length > 0,
      },
      fieldClass,
    ]"
  >
    <div class="input textarea" :style="{ height: height }">
      <quill-editor
        theme="snow"
        toolbar="minimal"
        v-bind="$attrs"
        v-model:content="localValue"
      >
      </quill-editor>
      <!-- <quill-editor theme="snow" toolbar="minimal"> </quill-editor> -->
      <!-- <textarea
        :value="modelValue"
        @input="$emit('update:modelValue', $event.target.value)"
        class="textarea__textarea"
        :class="{ 'not-empty': modelValue?.toString().length > 0 }"
        v-bind="$attrs"
      />
      <label class="textarea__label" v-html="label" :class="{ 'not-empty': modelValue?.toString().length > 0 }"></label> -->
    </div>
  </div>
</template>

<script type="text/javascript">
import "@vueup/vue-quill/dist/vue-quill.snow.css";
import { QuillEditor } from "@vueup/vue-quill";
import { computed } from "vue";

export default {
  name: "input-rich-text",
  components: {
    QuillEditor,
  },
  inheritAttrs: false,
  props: {
    modelValue: String,
    value: String,
    label: String,
    height: String,
    error: String,
    fieldClass: String,
    disabled: {
      type: Boolean,
      default: false,
    },
    requesting: {
      type: Boolean,
      default: false,
    },
    success: {
      type: Boolean,
      default: false,
    },
    // error: {
    //   type: String,
    //   default: "",
    // },
  },
  emits: ["update:modelValue"],
  setup: (props, ctx) => {
    const localValue = computed({
      get: () => props.modelValue,
      set: (content) => ctx.emit("update:modelValue", JSON.stringify(content)),
    });
    return {
      localValue,
    };
  },
};
</script>
