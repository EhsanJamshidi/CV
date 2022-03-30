<template>
  <div class="pdf-content">
    <cvpreview
      :personal-details="personalDetails"
      :skills="skills"
      :soft-skills="softSkills"
      :languages="languages"
      :languages-levels="languagesLevels"
      :experience="experience"
      :education="education"
      :projects="projects"
    />
  </div>
</template>

<script>
import cvpreview from '@/components/cvpreview.vue'
export default {
  name: 'Pdf',
  components: { cvpreview },
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
    return {}
  },
  computed: {},
  mounted() {},
}
</script>
