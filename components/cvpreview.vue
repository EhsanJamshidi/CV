<template>
  <div>
    <v-card v-if="personalDetails" class="ma-auto cv-preview" tile>
      <v-row class="ma-0 fill-height">
        <!-- personal details -->
        <v-col cols="4" class="pa-4 grey lighten-4 self-stretch">
          <v-row class="ma-0" align="start" justify="start">
            <v-col cols="12" class="pa-0 pt-4">
              <h2>
                {{ personalDetails.firstName }}
                {{ personalDetails.lastName }}
              </h2>
              <h3 class="blue--text text--darken-3">
                {{ personalDetails.jobTitle }}
              </h3>
              <p v-if="personalDetails.birthday" class="ma-0 text-left body-2">
                Born in
                <span>{{ personalDetails.birthday }}</span>
              </p>
              <p v-if="personalDetails.location" class="ma-0 text-left body-2">
                <span>{{ personalDetails.location }}</span>
              </p>
              <p v-if="personalDetails.email" class="ma-0 body-2">
                <v-icon color="blue darken-3" size="18">mdi-at</v-icon>
                <span>{{ personalDetails.email }}</span>
              </p>
              <p v-if="personalDetails.cellphone" class="ma-0 body-2">
                <v-icon color="blue darken-3" size="18">mdi-cellphone</v-icon>
                <span>{{ personalDetails.cellphone }}</span>
              </p>
              <p v-if="personalDetails.linkedIn" class="ma-0 body-2">
                <v-icon color="blue darken-3" size="18">mdi-linkedin</v-icon>
                <a
                  :href="personalDetails.linkedIn"
                  target="_blank"
                  style="text-decoration: none"
                  >LinkedIn</a
                >
              </p>
              <p v-if="personalDetails.twitter" class="ma-0 body-2">
                <v-icon color="blue darken-3" size="18">mdi-twitter</v-icon>
                <a
                  :href="personalDetails.twitter"
                  target="_blank"
                  style="text-decoration: none"
                  >Twitter</a
                >
              </p>
              <p v-if="personalDetails.github" class="ma-0 body-2">
                <v-icon color="blue darken-3" size="18">mdi-github</v-icon>
                <a
                  :href="personalDetails.github"
                  target="_blank"
                  style="text-decoration: none"
                  >Github</a
                >
              </p>
              <p v-if="personalDetails.website" class="ma-0 body-2">
                <v-icon color="blue darken-3" size="18">mdi-web</v-icon>
                <a
                  :href="personalDetails.website"
                  target="_blank"
                  style="text-decoration: none"
                  >Website</a
                >
              </p>
            </v-col>
            <!-- skills -->
            <v-col cols="12" class="pa-0 pt-3">
              <h4 class="blue--text text--darken-3">SKILLS</h4>
            </v-col>
            <v-col
              v-for="(item, i) in skills"
              :key="i + 1000"
              cols="auto"
              style="width: 90px"
              class="px-2 py-1"
            >
              <span class="body-2">
                {{ item.text }}
                <v-progress-linear
                  :value="item.value"
                  size="18"
                  width="2"
                  color="black"
                ></v-progress-linear>
              </span>
            </v-col>
            <!-- soft skills -->
            <v-col cols="12" class="pa-0 pt-3">
              <h4 class="blue--text text--darken-3">SOFT SKILLS</h4>
            </v-col>
            <v-col
              v-for="(item, i) in softSkills"
              :key="i + 1100"
              cols="12"
              class="px-1 py-0"
            >
              <span class="body-2">
                <span>
                  <v-icon color="black" size="6"
                    >mdi-checkbox-blank-circle</v-icon
                  >
                </span>
                {{ item.text }}
              </span>
            </v-col>
            <!-- languages -->
            <v-col cols="12" class="pa-0 pt-3">
              <h4 class="blue--text text--darken-3">LANGUAGES</h4>
            </v-col>
            <v-col
              v-for="(item, i) in languages"
              :key="i + 1200"
              cols="12"
              class="px-1 py-0"
            >
              <span class="body-2">
                <span>
                  <v-icon color="black" size="6"
                    >mdi-checkbox-blank-circle</v-icon
                  >
                </span>
                <span class="font-weight-black">{{ item.text }}: </span>
                <span class="text-italic">{{
                  languagesLevels.find((s) => s.value === item.value).text
                }}</span>
              </span>
            </v-col>
          </v-row>
          <!-- education -->
          <v-row v-if="education.length" class="ma-0" align="center">
            <v-col cols="12" class="pa-0 pt-3">
              <h4 class="blue--text text--darken-3">EDUCATION</h4>
            </v-col>
            <v-col
              v-for="(item, i) in education"
              :key="i + 800"
              cols="12"
              class="px-1 py-0"
            >
              <p class="ma-0 body-2 font-weight-black">
                <span>
                  <v-icon color="black" size="6"
                    >mdi-checkbox-blank-circle</v-icon
                  >
                </span>
                {{ item.field }}
              </p>
              <p class="ml-4 ma-0 body-2">{{ item.university }}</p>
              <p class="ml-4 ma-0 body-2">{{ item.location }}</p>
              <p class="ml-4 ma-0 body-2">{{ item.from }} - {{ item.to }}</p>
            </v-col>
          </v-row>
        </v-col>
        <v-col cols="8" class="pt-6 px-5">
          <v-row v-if="personalDetails.summary" class="ma-0" align="center">
            <v-col cols="12" class="pa-0 pt-3">
              <h4 class="blue--text text--darken-3">Summary</h4>
            </v-col>
            <v-col cols="12" class="px-1 py-0">
              <div class="text-justify" v-html="personalDetails.summary"></div>
            </v-col>
          </v-row>
          <!-- experience -->
          <v-row class="ma-0" align="center">
            <v-col cols="12" class="pa-0 pt-3">
              <h4 class="blue--text text--darken-3">EXPERIENCE</h4>
            </v-col>
            <v-col
              v-for="(item, i) in experience"
              :key="i + 700"
              cols="12"
              class="px-1 py-0"
            >
              <p class="ma-0">
                <span class="font-weight-bold">{{ item.title }}</span
                >,
                <span class="">
                  <a
                    :href="item.url"
                    target="_blank"
                    style="text-decoration: none"
                    >{{ item.company }}</a
                  ></span
                >,
                <span class="">{{ item.location }}</span>
              </p>
              <p class="ma-0 body-2">
                <span class="">{{ item.from }}</span> -
                <span v-if="item.to" class="">{{ item.to }}</span>
                <span v-if="item.ongoing" class="">PRESENT</span>
              </p>
              <div class="body-2" v-html="item.summary"></div>
            </v-col>
          </v-row>
          <!-- projects -->
          <v-row v-if="projects.length" class="ma-0" align="center">
            <v-col cols="12" class="pb-0">
              <h4 class="blue--text text--darken-3">PROJECTS</h4>
            </v-col>
            <v-col v-for="(item, i) in projects" :key="i + 900" cols="12">
              <p class="ma-0">
                <span class="font-weight-bold">{{ item.title }}</span
                >,
                <span class="">
                  <a
                    :href="item.url"
                    target="_blank"
                    style="text-decoration: none"
                    >{{ item.company }}</a
                  ></span
                >,
                <span class="">{{ item.location }}</span>
              </p>
              <p class="ma-0 body-2">
                <span class="">{{ item.from }}</span> -
                <span v-if="item.to" class="">{{ item.to }}</span>
                <span v-if="item.ongoing" class="">PRESENT</span>
              </p>
              <div class="body-2" v-html="item.summary"></div>
            </v-col>
          </v-row>
        </v-col>
      </v-row>
    </v-card>
  </div>
</template>

<script>
export default {
  name: 'Cvpreview',
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
  methods: {},
}
</script>

