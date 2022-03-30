<template>
  <div>
    <client-only>
      <vue-html2pdf
        ref="html2Pdf"
        :show-layout="false"
        :float-layout="true"
        :enable-download="true"
        :preview-modal="true"
        :paginate-elements-by-height="1400"
        filename="Resume"
        :pdf-quality="2"
        :manual-pagination="false"
        pdf-format="a4"
      >
        <pdf
          slot="pdf-content"
          :personal-details="personalDetails"
          :skills="skills"
          :soft-skills="softSkills"
          :languages="languages"
          :languages-levels="languagesLevels"
          :experience="experience"
          :education="education"
          :projects="projects"
          @domRendered="domRendered()"
        />
      </vue-html2pdf>
    </client-only>
    <div>
      <v-btn depressed class="info" @click="generate()">Get PDF</v-btn>
    </div>
  </div>
</template>
<script>
import pdf from '~/components/pdf.vue'
export default {
  name: 'Htmlpdf',
  components: { pdf },
  props: {
    personalDetails: { default: null, type: Object },
    skills: { default: null, type: Array },
    softSkills: { default: null, type: Array },
    languages: { default: null, type: Array },
    languagesLevels: { default: null, type: Array },
    experience: { default: null, type: Array },
    education: { default: null, type: Array },
    projects: { default: null, type: Array },
  },
  data() {
    return {
      body: {},
    }
  },
  watch: {},
  created() {},
  methods: {
    generate() {
      this.$refs.html2Pdf.generatePdf()
    },
  },
}
</script>
<style scoped>
</style>
