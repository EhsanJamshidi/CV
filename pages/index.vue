<template>
  <v-row class="ma-0 fill-height" justify="start" align="start">
    <v-col
      cols="12"
      sm="6"
      md="6"
      lg="5"
      xl="4"
      class="noprint blue-grey lighten-5 align-self-stretch"
    >
      <v-row class="ma-0" align="center">
        <v-col cols="" class="px-0">
          <h2 class="font-weight-light">CV Settings</h2>
        </v-col>
        <v-col cols="auto" class="px-0">
          <v-btn color="primary" @click="downloadPdf()">GET PDF</v-btn>
          <!-- <htmlpdf
            :personal-details="personalDetails"
            :skills="skills"
            :soft-skills="softSkills"
            :languages="languages"
            :languages-levels="languagesLevels"
            :experience="experience"
            :education="education"
            :projects="projects"
          /> -->
        </v-col>
        <v-col cols="12" class="pa-0">
          <v-expansion-panels>
            <v-expansion-panel>
              <v-expansion-panel-header>
                <h3 class="font-weight-regular">Personal Details</h3>
              </v-expansion-panel-header>
              <v-expansion-panel-content>
                <v-card class="py-3" flat outlined>
                  <v-row class="ma-0">
                    <v-col cols="12" md="6" class="py-0">
                      <v-text-field
                        v-model="personalDetails.firstName"
                        hide-details
                        class="mb-2"
                        dense
                        label="First Name"
                        required
                        outlined
                      ></v-text-field>
                    </v-col>
                    <v-col cols="12" md="6" class="py-0">
                      <v-text-field
                        v-model="personalDetails.lastName"
                        hide-details
                        class="mb-2"
                        dense
                        label="Last Name"
                        required
                        outlined
                      ></v-text-field>
                    </v-col>
                    <v-col cols="12" md="6" class="py-0">
                      <v-text-field
                        v-model="personalDetails.jobTitle"
                        hide-details
                        class="mb-2"
                        dense
                        label="Job Title"
                        required
                        outlined
                      ></v-text-field>
                    </v-col>
                    <v-col cols="12" md="6" class="py-0">
                      <v-text-field
                        v-model="personalDetails.location"
                        hide-details
                        class="mb-2"
                        dense
                        label="Location"
                        required
                        outlined
                      ></v-text-field>
                    </v-col>
                    <v-col cols="12" md="6" class="py-0">
                      <v-text-field
                        v-model="personalDetails.email"
                        hide-details
                        class="mb-2"
                        dense
                        label="E-mail"
                        required
                        outlined
                      ></v-text-field>
                    </v-col>
                    <v-col cols="12" md="6" class="py-0">
                      <v-text-field
                        v-model="personalDetails.cellphone"
                        hide-details
                        class="mb-2"
                        dense
                        label="Phone"
                        required
                        outlined
                      ></v-text-field>
                    </v-col>
                    <v-col cols="12" md="6" class="py-0">
                      <v-text-field
                        v-model="personalDetails.linkedIn"
                        hide-details
                        class="mb-2"
                        dense
                        label="LinkedIn"
                        required
                        outlined
                      ></v-text-field>
                    </v-col>
                    <v-col cols="12" md="6" class="py-0">
                      <v-text-field
                        v-model="personalDetails.twitter"
                        hide-details
                        class="mb-2"
                        dense
                        label="Twitter"
                        required
                        outlined
                      ></v-text-field>
                    </v-col>
                    <v-col cols="12" md="6" class="py-0">
                      <v-text-field
                        v-model="personalDetails.github"
                        hide-details
                        class="mb-2"
                        dense
                        label="Github"
                        required
                        outlined
                      ></v-text-field>
                    </v-col>
                    <v-col cols="12" md="6" class="py-0">
                      <v-text-field
                        v-model="personalDetails.website"
                        hide-details
                        class="mb-2"
                        dense
                        label="Website"
                        required
                        outlined
                      ></v-text-field>
                    </v-col>
                    <v-col cols="12" class="py-0">
                      <p class="mb-1">Summary:</p>
                      <editor
                        v-model="personalDetails.summary"
                        :maincontent="personalDetails.summary"
                      />
                    </v-col>
                  </v-row>
                </v-card>
              </v-expansion-panel-content>
            </v-expansion-panel>
            <v-expansion-panel>
              <v-expansion-panel-header>
                <h3 class="font-weight-regular">Skills</h3>
              </v-expansion-panel-header>
              <v-expansion-panel-content>
                <div v-for="(item, i) in skills" :key="i + 100">
                  <v-row class="ma-0" align="center">
                    <v-col cols="5" class="py-0">
                      <v-text-field
                        v-model="item.text"
                        hide-details
                        class="mb-2"
                        dense
                        label="Title"
                        required
                        outlined
                      ></v-text-field>
                    </v-col>
                    <v-col cols="5" class="py-0">
                      <v-select
                        v-model="item.value"
                        :items="skillsLevels"
                        label="Level"
                        hide-details
                        class="mb-2"
                        dense
                        required
                        outlined
                      ></v-select>
                    </v-col>
                    <v-col cols="2" class="py-0">
                      <v-btn
                        class="mb-2"
                        depressed
                        icon
                        small
                        color="error"
                        @click="
                          skills = skills.filter((s) => s.text !== item.text)
                        "
                        ><v-icon>mdi-delete</v-icon></v-btn
                      >
                    </v-col>
                  </v-row>
                </div>
                <v-row class="ma-0" align="center">
                  <v-col cols="12" class="py-0">
                    <span>New Item</span>
                  </v-col>
                  <v-col cols="5" class="py-0">
                    <v-text-field
                      v-model="skillsSample.text"
                      hide-details
                      class="mb-2"
                      dense
                      label="Title"
                      required
                      outlined
                    ></v-text-field>
                  </v-col>
                  <v-col cols="5" class="py-0">
                    <v-select
                      v-model="skillsSample.value"
                      :items="skillsLevels"
                      label="Level"
                      hide-details
                      class="mb-2"
                      dense
                      required
                      outlined
                    ></v-select>
                  </v-col>
                  <v-col cols="2">
                    <v-btn
                      class="mb-2"
                      depressed
                      icon
                      small
                      color="success"
                      @click="
                        skillsSample.text !== ''
                          ? skills.find((s) => s.text === skillsSample.text)
                            ? (skillsAlert = 'This item exists!')
                            : (skills.push(
                                JSON.parse(JSON.stringify(skillsSample))
                              ),
                              (skillsSample.text = ''),
                              (skillsSample.level = 0))
                          : (skillsAlert = 'Please enter the title!')
                      "
                    >
                      <v-icon>mdi-plus</v-icon>
                    </v-btn>
                  </v-col>
                  <v-col v-if="skillsAlert !== ''" cols="12">
                    <v-alert shaped class="error white--text">
                      <v-icon color="white" @click="skillsAlert = ''"
                        >mdi-close</v-icon
                      >
                      <span>{{ skillsAlert }}</span>
                    </v-alert>
                  </v-col>
                </v-row>
              </v-expansion-panel-content>
            </v-expansion-panel>
            <v-expansion-panel>
              <v-expansion-panel-header>
                <h3 class="font-weight-regular">Soft Skills</h3>
              </v-expansion-panel-header>
              <v-expansion-panel-content>
                <div v-for="(item, i) in softSkills" :key="i + 200">
                  <v-row class="ma-0" align="center">
                    <v-col cols="10" class="py-0">
                      <v-text-field
                        v-model="item.text"
                        hide-details
                        class="mb-2"
                        dense
                        label="Title"
                        required
                        outlined
                      ></v-text-field>
                    </v-col>
                    <v-col cols="2" class="py-0">
                      <v-btn
                        class="mb-2"
                        depressed
                        icon
                        small
                        color="error"
                        @click="
                          skills = skills.filter((s) => s.text !== item.text)
                        "
                        ><v-icon>mdi-delete</v-icon></v-btn
                      >
                    </v-col>
                  </v-row>
                </div>
                <v-row class="ma-0" align="center">
                  <v-col cols="12" class="py-0">
                    <span>New Item</span>
                  </v-col>
                  <v-col cols="10" class="py-0">
                    <v-text-field
                      v-model="skillsSample.text"
                      hide-details
                      class="mb-2"
                      dense
                      label="Title"
                      required
                      outlined
                    ></v-text-field>
                  </v-col>
                  <v-col cols="2" class="py-0">
                    <v-btn
                      class="mb-2"
                      depressed
                      icon
                      small
                      color="success"
                      @click="
                        skillsSample.text !== ''
                          ? skills.find((s) => s.text === skillsSample.text)
                            ? (skillsAlert = 'This item exists!')
                            : (skills.push(
                                JSON.parse(JSON.stringify(skillsSample))
                              ),
                              (skillsSample.text = ''),
                              (skillsSample.level = 0))
                          : (skillsAlert = 'Please enter the title!')
                      "
                      ><v-icon>mdi-plus</v-icon></v-btn
                    >
                  </v-col>
                  <v-col v-if="skillsAlert !== ''" cols="12">
                    <v-alert shaped class="error white--text">
                      <v-icon color="white" @click="skillsAlert = ''"
                        >mdi-close</v-icon
                      >
                      <span>{{ skillsAlert }}</span>
                    </v-alert>
                  </v-col>
                </v-row>
              </v-expansion-panel-content>
            </v-expansion-panel>
            <v-expansion-panel>
              <v-expansion-panel-header>
                <h3 class="font-weight-regular">Languages</h3>
              </v-expansion-panel-header>
              <v-expansion-panel-content>
                <div v-for="(item, i) in languages" :key="i + 300">
                  <v-row class="ma-0" align="center">
                    <v-col cols="5" class="py-0">
                      <v-text-field
                        v-model="item.text"
                        hide-details
                        class="mb-2"
                        dense
                        label="Title"
                        required
                        outlined
                      ></v-text-field>
                    </v-col>
                    <v-col cols="5" class="py-0">
                      <v-select
                        v-model="item.value"
                        :items="languagesLevels"
                        label="Level"
                        hide-details
                        class="mb-2"
                        dense
                        required
                        outlined
                      ></v-select>
                    </v-col>
                    <v-col cols="2">
                      <v-btn
                        class="mb-2"
                        depressed
                        icon
                        small
                        color="error"
                        @click="
                          languages = languages.filter(
                            (s) => s.text !== item.text
                          )
                        "
                        ><v-icon>mdi-delete</v-icon></v-btn
                      >
                    </v-col>
                  </v-row>
                </div>
                <v-row class="ma-0" align="center">
                  <v-col cols="12" class="py-0">
                    <span>New Item</span>
                  </v-col>
                  <v-col cols="5" class="py-0">
                    <v-text-field
                      v-model="languagesSample.text"
                      hide-details
                      class="mb-2"
                      dense
                      label="Title"
                      required
                      outlined
                    ></v-text-field>
                  </v-col>
                  <v-col cols="5" class="py-0">
                    <v-select
                      v-model="languagesSample.value"
                      :items="languagesLevels"
                      label="Level"
                      hide-details
                      class="mb-2"
                      dense
                      required
                      outlined
                    ></v-select>
                  </v-col>
                  <v-col cols="2">
                    <v-btn
                      class="mb-2"
                      depressed
                      icon
                      small
                      color="success"
                      @click="
                        languagesSample.text !== ''
                          ? languages.find(
                              (s) => s.text === languagesSample.text
                            )
                            ? (languagesAlert = 'This item exists!')
                            : (languages.push(
                                JSON.parse(JSON.stringify(languagesSample))
                              ),
                              (languagesSample.text = ''),
                              (languagesSample.level = 0))
                          : (languagesAlert = 'Please enter the title!')
                      "
                      ><v-icon>mdi-plus</v-icon></v-btn
                    >
                  </v-col>
                  <v-col v-if="languagesAlert !== ''" cols="12">
                    <v-alert shaped class="error white--text">
                      <v-icon color="white" @click="languagesAlert = ''"
                        >mdi-close</v-icon
                      >
                      <span>{{ languagesAlert }}</span>
                    </v-alert>
                  </v-col>
                </v-row>
              </v-expansion-panel-content>
            </v-expansion-panel>
            <v-expansion-panel>
              <v-expansion-panel-header>
                <h3 class="font-weight-regular">Educations</h3>
              </v-expansion-panel-header>
              <v-expansion-panel-content>
                <v-card
                  v-for="(item, i) in education"
                  :key="i + 500"
                  flat
                  outlined
                  class="pt-3"
                >
                  <v-row class="ma-0" align="center">
                    <v-col cols="12" md="4" class="py-0">
                      <v-text-field
                        v-model="item.university"
                        hide-details
                        class="mb-2"
                        dense
                        label="University"
                        required
                        outlined
                      ></v-text-field>
                    </v-col>
                    <v-col cols="12" md="4" class="py-0">
                      <v-text-field
                        v-model="item.field"
                        hide-details
                        class="mb-2"
                        dense
                        label="Field"
                        required
                        outlined
                      ></v-text-field>
                    </v-col>
                    <v-col cols="12" md="4" class="py-0">
                      <v-text-field
                        v-model="item.location"
                        hide-details
                        class="mb-2"
                        dense
                        label="Location"
                        required
                        outlined
                      ></v-text-field>
                    </v-col>
                    <v-col cols="12" md="5" class="py-0">
                      <v-menu
                        v-model="item.fromMenu"
                        :close-on-content-click="false"
                        transition="scale-transition"
                        offset-y
                        max-width="290px"
                        min-width="auto"
                      >
                        <template #activator="{ on, attrs }">
                          <v-text-field
                            v-model="item.from"
                            label="From"
                            readonly
                            hide-details
                            class="mb-2"
                            dense
                            required
                            outlined
                            v-bind="attrs"
                            v-on="on"
                          ></v-text-field>
                        </template>
                        <v-date-picker
                          v-model="item.from"
                          type="month"
                          :show-current="false"
                          no-title
                          scrollable
                        >
                          <v-spacer></v-spacer>
                          <v-btn
                            text
                            color="primary"
                            @click="item.fromMenu = false"
                          >
                            Cancel
                          </v-btn>
                          <v-btn
                            text
                            color="primary"
                            @click="item.fromMenu = false"
                          >
                            OK
                          </v-btn>
                        </v-date-picker>
                      </v-menu>
                    </v-col>
                    <v-col cols="12" md="7" class="pl-0 py-0">
                      <v-row class="ma-0">
                        <v-col cols="auto" class="pa-0">
                          <v-checkbox
                            v-model="item.ongoing"
                            label="Ongoing"
                            hide-details
                            class="pt-2 ma-0"
                          ></v-checkbox>
                        </v-col>
                        <v-col cols="" class="pl-3 pa-0">
                          <v-menu
                            v-model="item.toMenu"
                            :close-on-content-click="false"
                            transition="scale-transition"
                            offset-y
                            max-width="290px"
                            min-width="auto"
                          >
                            <template #activator="{ on, attrs }">
                              <v-text-field
                                v-model="item.to"
                                label="To"
                                readonly
                                hide-details
                                class="mb-2"
                                dense
                                required
                                outlined
                                v-bind="attrs"
                                v-on="on"
                              ></v-text-field>
                            </template>
                            <v-date-picker
                              v-model="item.to"
                              type="month"
                              :show-current="false"
                              no-title
                              scrollable
                            >
                              <v-spacer></v-spacer>
                              <v-btn
                                text
                                color="primary"
                                @click="item.toMenu = false"
                              >
                                Cancel
                              </v-btn>
                              <v-btn
                                text
                                color="primary"
                                @click="item.toMenu = false"
                              >
                                OK
                              </v-btn>
                            </v-date-picker>
                          </v-menu>
                        </v-col>
                      </v-row>
                    </v-col>
                    <v-col cols="12" class="py-2 text-right">
                      <v-btn
                        class="mb-2"
                        depressed
                        icon
                        small
                        color="error"
                        @click="
                          education = education.filter(
                            (s) => s.text !== item.text
                          )
                        "
                        ><v-icon>mdi-delete</v-icon></v-btn
                      >
                    </v-col>
                  </v-row>
                </v-card>
                <v-card flat outlined class="mt-2 pt-3">
                  <v-col cols="12" class="py-0">
                    <span>New Item</span>
                  </v-col>
                  <v-row class="ma-0" align="center">
                    <v-col cols="12" md="4" class="py-0">
                      <v-text-field
                        v-model="educationSample.university"
                        hide-details
                        class="mb-2"
                        dense
                        label="University"
                        required
                        outlined
                      ></v-text-field>
                    </v-col>
                    <v-col cols="12" md="4" class="py-0">
                      <v-text-field
                        v-model="educationSample.field"
                        hide-details
                        class="mb-2"
                        dense
                        label="Field"
                        required
                        outlined
                      ></v-text-field>
                    </v-col>
                    <v-col cols="12" md="4" class="py-0">
                      <v-text-field
                        v-model="educationSample.location"
                        hide-details
                        class="mb-2"
                        dense
                        label="Location"
                        required
                        outlined
                      ></v-text-field>
                    </v-col>
                    <v-col cols="12" md="5" class="py-0">
                      <v-menu
                        v-model="educationSample.fromMenu"
                        :close-on-content-click="false"
                        transition="scale-transition"
                        offset-y
                        max-width="290px"
                        min-width="auto"
                      >
                        <template #activator="{ on, attrs }">
                          <v-text-field
                            v-model="educationSample.from"
                            label="From"
                            readonly
                            hide-details
                            class="mb-2"
                            dense
                            required
                            outlined
                            v-bind="attrs"
                            v-on="on"
                          ></v-text-field>
                        </template>
                        <v-date-picker
                          v-model="educationSample.from"
                          type="month"
                          :show-current="false"
                          no-title
                          scrollable
                        >
                          <v-spacer></v-spacer>
                          <v-btn
                            text
                            color="primary"
                            @click="educationSample.fromMenu = false"
                          >
                            Cancel
                          </v-btn>
                          <v-btn
                            text
                            color="primary"
                            @click="educationSample.fromMenu = false"
                          >
                            OK
                          </v-btn>
                        </v-date-picker>
                      </v-menu>
                    </v-col>
                    <v-col cols="12" md="7" class="pl-0 py-0">
                      <v-row class="ma-0">
                        <v-col cols="auto" class="pa-0">
                          <v-checkbox
                            v-model="educationSample.ongoing"
                            label="Ongoing"
                            hide-details
                            class="pa-0 pt-2 ma-0"
                          ></v-checkbox>
                        </v-col>
                        <v-col cols="" class="pl-3 pa-0">
                          <v-menu
                            v-model="educationSample.toMenu"
                            :close-on-content-click="false"
                            transition="scale-transition"
                            offset-y
                            max-width="290px"
                            min-width="auto"
                          >
                            <template #activator="{ on, attrs }">
                              <v-text-field
                                v-model="educationSample.to"
                                label="To"
                                readonly
                                hide-details
                                class="mb-2"
                                dense
                                required
                                outlined
                                v-bind="attrs"
                                v-on="on"
                              ></v-text-field>
                            </template>
                            <v-date-picker
                              v-model="educationSample.to"
                              type="month"
                              :show-current="false"
                              no-title
                              scrollable
                            >
                              <v-spacer></v-spacer>
                              <v-btn
                                text
                                color="primary"
                                @click="educationSample.toMenu = false"
                              >
                                Cancel
                              </v-btn>
                              <v-btn
                                text
                                color="primary"
                                @click="educationSample.toMenu = false"
                              >
                                OK
                              </v-btn>
                            </v-date-picker>
                          </v-menu>
                        </v-col>
                      </v-row>
                    </v-col>
                    <v-col cols="12" class="py-0 text-right">
                      <v-btn
                        class="mb-2"
                        depressed
                        icon
                        small
                        color="success"
                        @click="
                          educationSample.text !== ''
                            ? education.find(
                                (s) => s.text === educationSample.text
                              )
                              ? (educationAlert = 'This item exists!')
                              : (education.push(
                                  JSON.parse(JSON.stringify(educationSample))
                                ),
                                (educationSample.text = ''),
                                (educationSample.level = 0))
                            : (educationAlert = 'Please enter the title!')
                        "
                        ><v-icon>mdi-plus</v-icon></v-btn
                      >
                    </v-col>
                    <v-col v-if="educationAlert !== ''" cols="12">
                      <v-alert shaped class="error white--text">
                        <v-icon color="white" @click="educationAlert = ''"
                          >mdi-close</v-icon
                        >
                        <span>{{ educationAlert }}</span>
                      </v-alert>
                    </v-col>
                  </v-row>
                </v-card>
              </v-expansion-panel-content>
            </v-expansion-panel>
            <v-expansion-panel>
              <v-expansion-panel-header>
                <h3 class="font-weight-regular">Experiences</h3>
              </v-expansion-panel-header>
              <v-expansion-panel-content>
                <v-card
                  v-for="(item, i) in experience"
                  :key="i + 400"
                  flat
                  outlined
                  class="py-3"
                >
                  <v-row class="ma-0" align="center">
                    <v-col cols="12" md="6" class="py-0">
                      <v-text-field
                        v-model="item.company"
                        hide-details
                        class="mb-2"
                        dense
                        label="Company"
                        required
                        outlined
                      ></v-text-field>
                    </v-col>
                    <v-col cols="12" md="6" class="py-0">
                      <v-text-field
                        v-model="item.url"
                        hide-details
                        class="mb-2"
                        dense
                        label="URL"
                        required
                        outlined
                      ></v-text-field>
                    </v-col>
                    <v-col cols="12" md="6" class="py-0">
                      <v-text-field
                        v-model="item.title"
                        hide-details
                        class="mb-2"
                        dense
                        label="Title"
                        required
                        outlined
                      ></v-text-field>
                    </v-col>
                    <v-col cols="12" md="6" class="py-0">
                      <v-text-field
                        v-model="item.location"
                        hide-details
                        class="mb-2"
                        dense
                        label="Location"
                        required
                        outlined
                      ></v-text-field>
                    </v-col>
                    <v-col cols="12" md="5" class="py-0">
                      <v-menu
                        v-model="item.fromMenu"
                        :close-on-content-click="false"
                        transition="scale-transition"
                        offset-y
                        max-width="290px"
                        min-width="auto"
                      >
                        <template #activator="{ on, attrs }">
                          <v-text-field
                            v-model="item.from"
                            label="From"
                            readonly
                            hide-details
                            class="mb-2"
                            dense
                            required
                            outlined
                            v-bind="attrs"
                            v-on="on"
                          ></v-text-field>
                        </template>
                        <v-date-picker
                          v-model="item.from"
                          type="month"
                          :show-current="false"
                          no-title
                          scrollable
                        >
                          <v-spacer></v-spacer>
                          <v-btn
                            text
                            color="primary"
                            @click="item.fromMenu = false"
                          >
                            Cancel
                          </v-btn>
                          <v-btn
                            text
                            color="primary"
                            @click="item.fromMenu = false"
                          >
                            OK
                          </v-btn>
                        </v-date-picker>
                      </v-menu>
                    </v-col>
                    <v-col cols="12" md="7" class="pl-0 py-0">
                      <v-row class="ma-0">
                        <v-col cols="auto" class="pa-0">
                          <v-checkbox
                            v-model="item.ongoing"
                            label="Ongoing"
                            hide-details
                            class="pt-2 ma-0"
                          ></v-checkbox>
                        </v-col>
                        <v-col cols="" class="pl-3 pa-0">
                          <v-menu
                            v-model="item.toMenu"
                            :close-on-content-click="false"
                            transition="scale-transition"
                            offset-y
                            max-width="290px"
                            min-width="auto"
                          >
                            <template #activator="{ on, attrs }">
                              <v-text-field
                                v-model="item.to"
                                label="To"
                                readonly
                                hide-details
                                class="mb-2"
                                dense
                                required
                                outlined
                                v-bind="attrs"
                                v-on="on"
                              ></v-text-field>
                            </template>
                            <v-date-picker
                              v-model="item.to"
                              type="month"
                              :show-current="false"
                              no-title
                              scrollable
                            >
                              <v-spacer></v-spacer>
                              <v-btn
                                text
                                color="primary"
                                @click="item.toMenu = false"
                              >
                                Cancel
                              </v-btn>
                              <v-btn
                                text
                                color="primary"
                                @click="item.toMenu = false"
                              >
                                OK
                              </v-btn>
                            </v-date-picker>
                          </v-menu>
                        </v-col>
                      </v-row>
                    </v-col>
                    <v-col cols="12" class="pt-0">
                      <p class="ma-0">Summary:</p>
                      <editor
                        v-model="item.summary"
                        :maincontent="item.summary"
                      />
                    </v-col>
                    <v-col cols="12" class="text-right py-0">
                      <v-btn
                        class="ma-0"
                        depressed
                        icon
                        small
                        color="error"
                        @click="
                          experience = experience.iconr(
                            (s) => s.text !== item.text
                          )
                        "
                        ><v-icon>mdi-delete</v-icon></v-btn
                      >
                    </v-col>
                  </v-row>
                </v-card>
                <v-card class="mt-2 pt-3" flat outlined>
                  <v-row class="ma-0" align="center">
                    <v-col cols="12" class="py-0">
                      <span>New Item</span>
                    </v-col>
                    <v-col cols="12" md="6" class="py-0">
                      <v-text-field
                        v-model="experienceSample.company"
                        hide-details
                        class="mb-2"
                        dense
                        label="Company"
                        required
                        outlined
                      ></v-text-field>
                    </v-col>
                    <v-col cols="12" md="6" class="py-0">
                      <v-text-field
                        v-model="experienceSample.url"
                        hide-details
                        class="mb-2"
                        dense
                        label="URL"
                        required
                        outlined
                      ></v-text-field>
                    </v-col>
                    <v-col cols="12" md="6" class="py-0">
                      <v-text-field
                        v-model="experienceSample.title"
                        hide-details
                        class="mb-2"
                        dense
                        label="Title"
                        required
                        outlined
                      ></v-text-field>
                    </v-col>
                    <v-col cols="12" md="6" class="py-0">
                      <v-text-field
                        v-model="experienceSample.location"
                        hide-details
                        class="mb-2"
                        dense
                        label="Location"
                        required
                        outlined
                      ></v-text-field>
                    </v-col>
                    <v-col cols="12" md="5" class="py-0">
                      <v-menu
                        v-model="experienceSample.fromMenu"
                        :close-on-content-click="false"
                        transition="scale-transition"
                        offset-y
                        max-width="290px"
                        min-width="auto"
                      >
                        <template #activator="{ on, attrs }">
                          <v-text-field
                            v-model="experienceSample.from"
                            label="From"
                            readonly
                            hide-details
                            class="mb-2"
                            dense
                            required
                            outlined
                            v-bind="attrs"
                            v-on="on"
                          ></v-text-field>
                        </template>
                        <v-date-picker
                          v-model="experienceSample.from"
                          type="month"
                          :show-current="false"
                          no-title
                          scrollable
                        >
                          <v-spacer></v-spacer>
                          <v-btn
                            text
                            color="primary"
                            @click="experienceSample.fromMenu = false"
                          >
                            Cancel
                          </v-btn>
                          <v-btn
                            text
                            color="primary"
                            @click="experienceSample.fromMenu = false"
                          >
                            OK
                          </v-btn>
                        </v-date-picker>
                      </v-menu>
                    </v-col>
                    <v-col cols="12" md="7" class="pl-0 py-0">
                      <v-row class="ma-0">
                        <v-col cols="auto" class="pa-0">
                          <v-checkbox
                            v-model="experienceSample.ongoing"
                            label="Ongoing"
                            hide-details
                            class="pt-2 ma-0"
                          ></v-checkbox>
                        </v-col>
                        <v-col cols="" class="pl-3 pa-0">
                          <v-menu
                            v-model="experienceSample.toMenu"
                            :close-on-content-click="false"
                            transition="scale-transition"
                            offset-y
                            max-width="290px"
                            min-width="auto"
                          >
                            <template #activator="{ on, attrs }">
                              <v-text-field
                                v-model="experienceSample.to"
                                label="To"
                                readonly
                                hide-details
                                class="mb-2"
                                dense
                                required
                                outlined
                                v-bind="attrs"
                                v-on="on"
                              ></v-text-field>
                            </template>
                            <v-date-picker
                              v-model="experienceSample.to"
                              type="month"
                              :show-current="false"
                              no-title
                              scrollable
                            >
                              <v-spacer></v-spacer>
                              <v-btn
                                text
                                color="primary"
                                @click="experienceSample.toMenu = false"
                              >
                                Cancel
                              </v-btn>
                              <v-btn
                                text
                                color="primary"
                                @click="experienceSample.toMenu = false"
                              >
                                OK
                              </v-btn>
                            </v-date-picker>
                          </v-menu>
                        </v-col>
                      </v-row>
                    </v-col>
                    <v-col cols="12" class="pt-0">
                      <p class="ma-0">Summary:</p>
                      <editor
                        v-model="experienceSample.summary"
                        :maincontent="experienceSample.summary"
                      />
                    </v-col>
                    <v-col cols="12" class="text-right py-0">
                      <v-btn
                        class="mb-2"
                        depressed
                        icon
                        small
                        color="success"
                        @click="
                          experienceSample.text !== ''
                            ? experience.find(
                                (s) => s.text === experienceSample.text
                              )
                              ? (experienceAlert = 'This item exists!')
                              : (experience.push(
                                  JSON.parse(JSON.stringify(experienceSample))
                                ),
                                (experienceSample.text = ''),
                                (experienceSample.level = 0))
                            : (experienceAlert = 'Please enter the title!')
                        "
                        ><v-icon>mdi-plus</v-icon></v-btn
                      >
                    </v-col>
                    <v-col v-if="experienceAlert !== ''" cols="12">
                      <v-alert shaped class="error white--text">
                        <v-icon color="white" @click="experienceAlert = ''"
                          >mdi-close</v-icon
                        >
                        <span>{{ experienceAlert }}</span>
                      </v-alert>
                    </v-col>
                  </v-row>
                </v-card>
              </v-expansion-panel-content>
            </v-expansion-panel>
            <v-expansion-panel>
              <v-expansion-panel-header>
                <h3 class="font-weight-regular">Projects</h3>
              </v-expansion-panel-header>
              <v-expansion-panel-content>
                <v-card
                  v-for="(item, i) in projects"
                  :key="i + 600"
                  flat
                  outlined
                  class="py-3"
                >
                  <v-row class="ma-0" align="center">
                    <v-col cols="12" md="6" class="py-0">
                      <v-text-field
                        v-model="item.title"
                        hide-details
                        class="mb-2"
                        dense
                        label="Title"
                        required
                        outlined
                      ></v-text-field>
                    </v-col>
                    <v-col cols="12" md="6" class="py-0">
                      <v-text-field
                        v-model="item.url"
                        hide-details
                        class="mb-2"
                        dense
                        label="URL"
                        required
                        outlined
                      ></v-text-field>
                    </v-col>
                    <v-col cols="12" md="5" class="py-0">
                      <v-menu
                        v-model="item.fromMenu"
                        :close-on-content-click="false"
                        transition="scale-transition"
                        offset-y
                        max-width="290px"
                        min-width="auto"
                      >
                        <template #activator="{ on, attrs }">
                          <v-text-field
                            v-model="item.from"
                            label="From"
                            readonly
                            hide-details
                            class="mb-2"
                            dense
                            required
                            outlined
                            v-bind="attrs"
                            v-on="on"
                          ></v-text-field>
                        </template>
                        <v-date-picker
                          v-model="item.from"
                          type="month"
                          :show-current="false"
                          no-title
                          scrollable
                        >
                          <v-spacer></v-spacer>
                          <v-btn
                            text
                            color="primary"
                            @click="item.fromMenu = false"
                          >
                            Cancel
                          </v-btn>
                          <v-btn
                            text
                            color="primary"
                            @click="item.fromMenu = false"
                          >
                            OK
                          </v-btn>
                        </v-date-picker>
                      </v-menu>
                    </v-col>
                    <v-col cols="12" md="7" class="pl-0 py-0">
                      <v-row class="ma-0">
                        <v-col cols="auto" class="pa-0">
                          <v-checkbox
                            v-model="item.ongoing"
                            label="Ongoing"
                            hide-details
                            class="pt-2 ma-0"
                          ></v-checkbox>
                        </v-col>
                        <v-col cols="" class="pl-3 pa-0">
                          <v-menu
                            v-model="item.toMenu"
                            :close-on-content-click="false"
                            transition="scale-transition"
                            offset-y
                            max-width="290px"
                            min-width="auto"
                          >
                            <template #activator="{ on, attrs }">
                              <v-text-field
                                v-model="item.to"
                                label="To"
                                readonly
                                hide-details
                                class="mb-2"
                                dense
                                required
                                outlined
                                v-bind="attrs"
                                v-on="on"
                              ></v-text-field>
                            </template>
                            <v-date-picker
                              v-model="item.to"
                              type="month"
                              :show-current="false"
                              no-title
                              scrollable
                            >
                              <v-spacer></v-spacer>
                              <v-btn
                                text
                                color="primary"
                                @click="item.toMenu = false"
                              >
                                Cancel
                              </v-btn>
                              <v-btn
                                text
                                color="primary"
                                @click="item.toMenu = false"
                              >
                                OK
                              </v-btn>
                            </v-date-picker>
                          </v-menu>
                        </v-col>
                      </v-row>
                    </v-col>
                    <v-col cols="12" class="pt-0">
                      <p class="ma-0">Summary:</p>
                      <editor
                        v-model="item.summary"
                        :maincontent="item.summary"
                      />
                    </v-col>
                    <v-col cols="12" class="py-0 text-right">
                      <v-btn
                        class="mb-2"
                        depressed
                        icon
                        small
                        color="error"
                        @click="
                          projects = projects.filter(
                            (s) => s.text !== item.text
                          )
                        "
                        ><v-icon>mdi-delete</v-icon></v-btn
                      >
                    </v-col>
                  </v-row>
                </v-card>
                <v-card flat outlined class="mt-2 pt-3">
                  <v-row class="ma-0" align="center">
                    <v-col cols="12" class="py-0">
                      <span>New Item</span>
                    </v-col>
                    <v-col cols="12" md="6" class="py-0">
                      <v-text-field
                        v-model="projectsSample.title"
                        hide-details
                        class="mb-2"
                        dense
                        label="Title"
                        required
                        outlined
                      ></v-text-field>
                    </v-col>
                    <v-col cols="12" md="6" class="py-0">
                      <v-text-field
                        v-model="projectsSample.url"
                        hide-details
                        class="mb-2"
                        dense
                        label="URL"
                        required
                        outlined
                      ></v-text-field>
                    </v-col>
                    <v-col cols="12" md="5" class="py-0">
                      <v-menu
                        v-model="projectsSample.fromMenu"
                        :close-on-content-click="false"
                        transition="scale-transition"
                        offset-y
                        max-width="290px"
                        min-width="auto"
                      >
                        <template #activator="{ on, attrs }">
                          <v-text-field
                            v-model="projectsSample.from"
                            label="From"
                            readonly
                            hide-details
                            class="mb-2"
                            dense
                            required
                            outlined
                            v-bind="attrs"
                            v-on="on"
                          ></v-text-field>
                        </template>
                        <v-date-picker
                          v-model="projectsSample.from"
                          type="month"
                          :show-current="false"
                          no-title
                          scrollable
                        >
                          <v-spacer></v-spacer>
                          <v-btn
                            text
                            color="primary"
                            @click="projectsSample.fromMenu = false"
                          >
                            Cancel
                          </v-btn>
                          <v-btn
                            text
                            color="primary"
                            @click="projectsSample.fromMenu = false"
                          >
                            OK
                          </v-btn>
                        </v-date-picker>
                      </v-menu>
                    </v-col>
                    <v-col cols="12" md="7" class="pl-0 py-0">
                      <v-row class="ma-0">
                        <v-col cols="auto" class="pa-0">
                          <v-checkbox
                            v-model="projectsSample.ongoing"
                            label="Ongoing"
                            hide-details
                            class="pt-2 ma-0"
                          ></v-checkbox>
                        </v-col>
                        <v-col cols="" class="pl-3 pa-0">
                          <v-menu
                            v-model="projectsSample.toMenu"
                            :close-on-content-click="false"
                            transition="scale-transition"
                            offset-y
                            max-width="290px"
                            min-width="auto"
                          >
                            <template #activator="{ on, attrs }">
                              <v-text-field
                                v-model="projectsSample.to"
                                label="To"
                                readonly
                                hide-details
                                class="mb-2"
                                dense
                                required
                                outlined
                                v-bind="attrs"
                                v-on="on"
                              ></v-text-field>
                            </template>
                            <v-date-picker
                              v-model="projectsSample.to"
                              type="month"
                              :show-current="false"
                              no-title
                              scrollable
                            >
                              <v-spacer></v-spacer>
                              <v-btn
                                text
                                color="primary"
                                @click="projectsSample.toMenu = false"
                              >
                                Cancel
                              </v-btn>
                              <v-btn
                                text
                                color="primary"
                                @click="projectsSample.toMenu = false"
                              >
                                OK
                              </v-btn>
                            </v-date-picker>
                          </v-menu>
                        </v-col>
                      </v-row>
                    </v-col>
                    <v-col cols="12" class="pt-0">
                      <p class="ma-0">Summary:</p>
                      <editor
                        v-model="projectsSample.summary"
                        :maincontent="projectsSample.summary"
                      />
                    </v-col>
                    <v-col cols="12" class="py-0 text-right">
                      <v-btn
                        class="mb-0"
                        depressed
                        icon
                        small
                        color="success"
                        @click="
                          projectsSample.text !== ''
                            ? projects.find(
                                (s) => s.text === projectsSample.text
                              )
                              ? (projectsAlert = 'This item exists!')
                              : (projects.push(
                                  JSON.parse(JSON.stringify(projectsSample))
                                ),
                                (projectsSample.text = ''),
                                (projectsSample.level = 0))
                            : (projectsAlert = 'Please enter the title!')
                        "
                        ><v-icon>mdi-plus</v-icon></v-btn
                      >
                    </v-col>
                    <v-col v-if="projectsAlert !== ''" cols="12">
                      <v-alert shaped class="error white--text">
                        <v-icon color="white" @click="projectsAlert = ''"
                          >mdi-close</v-icon
                        >
                        <span>{{ projectsAlert }}</span>
                      </v-alert>
                    </v-col>
                  </v-row>
                </v-card>
              </v-expansion-panel-content>
            </v-expansion-panel>
          </v-expansion-panels>
        </v-col>
      </v-row>
    </v-col>
    <v-col cols="12" sm="6" md="6" lg="7" xl="8" class="pa-0 grey lighten-5">
      <cvpreview
        :personal-details="personalDetails"
        :skills="skills"
        :soft-skills="softSkills"
        :languages="languages"
        :experience="experience"
        :education="education"
        :projects="projects"
        :languages-levels="languagesLevels"
      />
    </v-col>
  </v-row>
</template>
<script>
// import Htmlpdf from '../components/htmlpdf.vue'
import editor from '@/components/editor.vue'
import cvpreview from '@/components/cvpreview.vue'
export default {
  components: {
    editor,
    cvpreview,
    // Htmlpdf //
  },
  data: () => ({
    personalDetails: {
      jobTitle: 'Web Developer',
      location: 'Tehran, Iran',
      firstName: 'Ehsan',
      lastName: 'Jamshidi',
      birthday: 'January 1992',
      email: 'ehsan.jamshidiii@gmail.com',
      cellphone: '00989127523642',
      linkedIn: 'www.linkedin.com/in/ehsan-jamshidi-095886183',
      twitter: '',
      github: '',
      website: '',
      summary:
        "In the past eight years, I worked as a Web Developer. I learned how to deal with different challenges that give me a lot of experience in how to handle every aspect of websites such as Server, APIs, Database, PWA, SEO, Speed and etc. I've also learned how to create algorithms to use lower resources with high-speed execution.",
    },
    skills: [
      {
        text: 'PHP',
        value: '100',
      },
      {
        text: 'Laravel',
        value: '100',
      },
      {
        text: 'MySQL',
        value: '100',
      },
      {
        text: 'JavaScript',
        value: '100',
      },
      {
        text: 'VueJS',
        value: '100',
      },
      {
        text: 'NuxtJS',
        value: '100',
      },
      {
        text: 'Vuetify',
        value: '100',
      },
      {
        text: 'HTML',
        value: '100',
      },
      {
        text: 'CSS',
        value: '100',
      },
      {
        text: 'SASS',
        value: '100',
      },
      {
        text: 'Bootstrap',
        value: '100',
      },
      {
        text: 'MS SQL',
        value: '100',
      },
      {
        text: 'Rest API',
        value: '100',
      },
      {
        text: 'Phalcon',
        value: '100',
      },
      {
        text: 'NodeJS',
        value: '75',
      },
      {
        text: 'TypeScript',
        value: '50',
      },
      {
        text: 'ExpressJS',
        value: '50',
      },
      {
        text: 'NestJS',
        value: '50',
      },
      {
        text: 'Git',
        value: '50',
      },
      {
        text: 'MVC',
        value: '100',
      },
      {
        text: 'SEO',
        value: '50',
      },
    ],
    skillsSample: {
      text: '',
      value: 0,
    },
    skillsLevels: [
      {
        text: 'Novice',
        value: '0',
      },
      {
        text: 'Beginner',
        value: '25',
      },
      {
        text: 'Intermediate',
        value: '50',
      },
      {
        text: 'Proficient',
        value: '75',
      },
      {
        text: 'Expert',
        value: '100',
      },
    ],
    skillsAlert: '',
    softSkills: [
      {
        text: 'Analytical mind',
      },
      {
        text: 'Creativity',
      },
      {
        text: 'Flexibility',
      },
      {
        text: 'Open-mindedness',
      },
      {
        text: 'Attention to Detail',
      },
    ],
    softSkillsSample: {
      text: '',
    },
    softSkillsSampleAlert: '',
    languages: [
      {
        text: 'Persain',
        value: '100',
      },
      {
        text: 'English',
        value: '50',
      },
    ],
    languagesSample: {
      text: '',
      value: '',
    },
    languagesLevels: [
      {
        text: 'Novice',
        value: '0',
      },
      {
        text: 'Basic',
        value: '25',
      },
      {
        text: 'Conversational',
        value: '50',
      },
      {
        text: 'Proficient',
        value: '75',
      },
      {
        text: 'Fluent',
        value: '100',
      },
    ],
    languagesAlert: '',
    experience: [
      {
        company: 'Damsaz Shop',
        url: 'https://damsaz.kitchen/shop',
        title: 'Full Stack Web Developer',
        location: 'Tehran, Iran',
        from: 'Januray 2022',
        fromMenu: false,
        to: '',
        toMenu: false,
        ongoing: true,
        summary:
          '<ul><li>Prepare an online shop core for industrial kitchen equipment.</li><li>Salesmen service to manage their workers and all the sales progress step by step to provide consulting to their customers.</li></ul>',
      },
      {
        company: 'Chatreto',
        url: 'https://chatreto.com',
        title: 'Full Stack Web Developer',
        location: 'Tehran, Iran',
        from: 'July 2021',
        fromMenu: false,
        to: 'December 2021',
        toMenu: false,
        ongoing: false,
        summary:
          '<ul><li>Built PWA app for insurance order service of 8 different types.</li><li>Implement forms with an Auto-generate structure based on the API to increase reusability.</li></ul>',
      },
      {
        company: 'EshelTeam',
        url: 'https://eshelteam.com',
        title: 'Full Stack Web Developer',
        location: 'Tehran, Iran',
        from: 'September 2020',
        fromMenu: false,
        to: 'November 2020',
        toMenu: false,
        ongoing: false,
        summary:
          '<ul><li>High-speed industrial kitchen category that helps the company to get half of their links on the first page of SERP.</li></ul>',
      },
      {
        company: 'Sports Data Analyzer',
        url: '',
        title: 'Full Stack Web Developer',
        location: 'Canada',
        from: 'December 2019',
        fromMenu: false,
        to: 'December 2021',
        toMenu: false,
        ongoing: false,
        summary:
          '<ul><li>Design a compiler on more than 50 different APIs (JSON, XML, etc.)  so all data would have an equal JSON format output.</li><li>Built an algorithm with 5 different stages of comparing and updating the database to compare all outputs with the database.</li><li>Design and implement a database with SQL Server and in-memory table to increase the speed of process for comparing and updating more than 20 million rows in under 1 minute.</li><li>Create an administrator panel (PWA) to handle all APIs and analyze formulas.</li><li>Prepare the whole website as PWA to operate and publicly show all analyzed data to users with different needs. Handel more than 5000 events every week.</li></ul>',
      },
      {
        company: 'Damsaz',
        url: 'https://damsaz.kitchen',
        title: 'Full Stack Web Developer',
        location: 'Tehran, Iran',
        from: 'July 2018',
        fromMenu: false,
        to: 'November 2021',
        toMenu: false,
        ongoing: false,
        summary:
          '<ul><li>Build specific CMS  for an online category list of the industrial kitchen equipment company. it took around 45 days to design a database and create individual CMS.</li><li>In late 2021 Upgrade the CMS to increase their visits to double by reconfiguring the database and URL list, also updating UI / UX for their benefits.</li></ul>',
      },
      {
        company: 'Saman4149',
        url: 'https://saman4149.com',
        title: 'Full Stack Web Developer',
        location: 'Tehran, Iran',
        from: 'July 2018',
        fromMenu: false,
        to: 'September 2018',
        toMenu: false,
        ongoing: false,
        summary:
          '<ul><li>Prepared individual CMS for an insurance agency that gains visits and increases its revenue.</li><li>Design online insurance orders process based on Company API. that leads to monthly revenue.</li></ul>',
      },
    ],
    experienceSample: {
      company: '',
      url: '',
      title: '',
      location: '',
      from: '',
      fromMenu: false,
      to: '',
      toMenu: false,
      ongoing: false,
      summary: '',
    },
    experienceAlert: '',
    education: [
      {
        university: 'Shahid Shamsipour',
        field: 'Software Engineering',
        location: 'Tehran, Iran',
        from: 'Jan 2011',
        to: 'Jan 2015',
        fromMenu: false,
        toMenu: false,
        ongoing: false,
      },
    ],
    educationSample: {
      university: '',
      field: '',
      location: '',
      from: '',
      to: '',
      fromMenu: false,
      toMenu: false,
      ongoing: false,
    },
    educationAlert: '',
    projects: [],
    projectsSample: {
      title: '',
      url: '',
      from: '',
      to: '',
      fromMenu: false,
      toMenu: false,
      ongoing: false,
      summary: '',
    },
    projectsAlert: '',
  }),
  head() {
    return {
      title:
        this.personalDetails.firstName +
        ' ' +
        this.personalDetails.lastName +
        ' - Resume',
      meta: [
        {
          hid: 'description',
          name: 'description',
          content:
            this.personalDetails.firstName +
            ' ' +
            this.personalDetails.lastName +
            ' - Resume',
        },
      ],
    }
  },
  created() {},
  methods: {
    downloadPdf() {
      window.print()
    },
  },
}
</script>
