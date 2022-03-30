<template>
  <div>
    <client-only>
      <VueEditor
        id="editor"
        v-model="content"
        use-custom-image-handler
        :editor-toolbar="customToolbar"
        :editor-options="editorSettings"
        @input="handleInput"
      />
    </client-only>
  </div>
</template>

<script>
export default {
  name: 'Editor',
  props: {
    maincontent: { default: '', type: String },
  },
  data() {
    return {
      content: '',
      customToolbar: [
        // [{ direction: 'rtl' }], // text direction
        // [{ align: [] }],
        [
          { align: '' },
          { align: 'justify' },
          { align: 'center' },
          { align: 'right' },
        ],
        [{ header: [1, 2, 3, 4, 5, 6, false] }],
        ['strike', 'underline', 'italic', 'bold'], // toggled buttons
        [{ color: [] }, { background: [] }], // dropdown with defaults from theme
        [{ list: 'ordered' }, { list: 'bullet' }],
        // ['code', 'blockquote', 'code-block'],
        // [{ script: 'sub' }, { script: 'super' }], // superscript/subscript
        [{ indent: '-1' }, { indent: '+1' }], // outdent/indent
        ['clean'],
      ],
      editorSettings: { format: { direction: 'rtl' } },
    }
  },
  watch: {
    maincontent(newVal) {
      this.content = newVal
    },
  },
  created() {
    this.content = this.maincontent
  },
  methods: {
    handleInput() {
      this.$emit('input', this.content)
    },
  },
}
</script>
