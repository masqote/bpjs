<template>
  <div class="pb-20">
    <!-- PERSONAL DETAILS -->
    <div class="p-10 space-y-2">
      <div>
        <h3 class="font-bold text-xl">Personal Details</h3>
      </div>
      <div class="space-x-6 w-full flex flex-row justify-center">
        <div class="flex flex-col space-y-2 w-1/2">
          <div class="pt-4 flex flex-row space-x-2 items-center">
            <label class="text-gray-400 text-sm">Wanted Job Title</label>
            <TooltipsDefault text="Pekerjaan apa yang anda inginkan ?" />
          </div>
          <div>
            <InputText v-model="form.jobTitle" required />
          </div>
        </div>
        <div class="flex flex-row items-center space-y-2 w-1/2">
          <div class="w-1/4 h-full flex items-end">
            <div
              class="h-3/4 bg-gray-300 w-16 rounded flex items-center justify-center"
            >
              <img src="~/assets/svg/user.svg" class="w-8 h-8" />
            </div>
          </div>
          <div class="w-3/4 pt-4 px-2">
            <input
              @change="uploadPhoto"
              type="file"
              ref="photo"
              class="hidden"
            />
            <div class="flex flex-col items-start">
              <div
                class="flex flex-row items-center space-x-3"
                v-if="form.photo"
              >
                <span>{{ form.photo.name }}</span>
                <span
                  @click="form.photo = null"
                  class="cursor-pointer text-red-600 border -mt-4 px-2"
                  >x</span
                >
              </div>
              <button
                class="text-sm text-blue-400"
                @click="$refs['photo'].click()"
              >
                {{ form.photo ? 'Change Photo' : 'Upload Photo' }}
              </button>
              <div v-show="validate.photo" class="text-red-600 text-sm">
                Photo hanya dalam format image!
              </div>
            </div>
          </div>
        </div>
      </div>

      <div class="space-x-6 w-full flex flex-row justify-center">
        <div class="flex flex-col space-y-2 w-1/2">
          <div class="pt-4 flex flex-row space-x-2 items-center">
            <label class="text-gray-400 text-sm">First Name</label>
          </div>
          <div>
            <InputText v-model="form.firstName" required />
          </div>
        </div>
        <div class="flex flex-col space-y-2 w-1/2">
          <div class="pt-4 flex flex-row space-x-2 items-center">
            <label class="text-gray-400 text-sm">Last Name</label>
          </div>
          <div>
            <InputText v-model="form.lastName" required />
          </div>
        </div>
      </div>

      <div class="space-x-6 w-full flex flex-row justify-center">
        <div class="flex flex-col space-y-2 w-1/2">
          <div class="pt-4 flex flex-row space-x-2 items-center">
            <label class="text-gray-400 text-sm">Email</label>
          </div>
          <div>
            <InputText type="email" required />
          </div>
        </div>
        <div class="flex flex-col space-y-2 w-1/2">
          <div class="pt-4 flex flex-row space-x-2 items-center">
            <label class="text-gray-400 text-sm">Phone</label>
          </div>
          <div>
            <InputNumber :min="3" :max="13" required />
          </div>
        </div>
      </div>

      <div class="space-x-6 w-full flex flex-row justify-center">
        <div class="flex flex-col space-y-2 w-1/2">
          <div class="pt-4 flex flex-row space-x-2 items-center">
            <label class="text-gray-400 text-sm">Country</label>
          </div>
          <div>
            <InputSelect
              v-model="form.country"
              :resources="countries"
              placeholder="Choose Country"
              required
            />
          </div>
        </div>
        <div class="flex flex-col space-y-2 w-1/2">
          <div class="pt-4 flex flex-row space-x-2 items-center">
            <label class="text-gray-400 text-sm">City</label>
          </div>
          <div>
            <InputSelect
              v-model="form.city"
              :resources="cities"
              placeholder="Choose City"
              required
            />
          </div>
        </div>
      </div>

      <div class="space-x-6 w-full flex flex-row justify-center">
        <div class="flex flex-col space-y-2 w-1/2">
          <div class="pt-4 flex flex-row space-x-2 items-center">
            <label class="text-gray-400 text-sm">Address</label>
          </div>
          <div>
            <InputText required />
          </div>
        </div>
        <div class="flex flex-col space-y-2 w-1/2">
          <div class="pt-4 flex flex-row space-x-2 items-center">
            <label class="text-gray-400 text-sm">Postal Code</label>
          </div>
          <div>
            <InputNumber :max="20" required />
          </div>
        </div>
      </div>

      <div class="space-x-6 w-full flex flex-row justify-center">
        <div class="flex flex-col space-y-2 w-1/2">
          <div class="pt-4 flex flex-row space-x-2 items-center">
            <label class="text-gray-400 text-sm">Driving License</label>
            <TooltipsDefault text="Masukkan nomor SIM / Surat Izin Mengemudi" />
          </div>
          <div>
            <InputNumber required />
          </div>
        </div>
        <div class="flex flex-col space-y-2 w-1/2">
          <div class="pt-4 flex flex-row space-x-2 items-center">
            <label class="text-gray-400 text-sm">Nationality</label>
            <TooltipsDefault text="Kewarganegaraan" />
          </div>
          <div>
            <InputText required />
          </div>
        </div>
      </div>

      <div class="space-x-6 w-full flex flex-row justify-center">
        <div class="flex flex-col space-y-2 w-1/2">
          <div class="pt-4 flex flex-row space-x-2 items-center">
            <label class="text-gray-400 text-sm">Place Of Birth</label>
          </div>
          <div>
            <InputText required />
          </div>
        </div>
        <div class="flex flex-col space-y-2 w-1/2">
          <div class="pt-4 flex flex-row space-x-2 items-center">
            <label class="text-gray-400 text-sm">Date Of Birth</label>
            <TooltipsDefault text="Format Tanggal : DD/MM/YYYY" />
          </div>
          <div>
            <InputDate required v-model="form.dateOfBirth" />
          </div>
        </div>
      </div>
    </div>

    <!-- PROFESSIONAL SUMMARY -->
    <div class="px-10 space-y-2">
      <div>
        <h3 class="font-bold text-xl">Professional Summary</h3>
        <p class="text-gray-400 text-sm">
          Write 2-4 short & energetic sentences to interest the reader! Mention
          your role,experience & most importantly - your biggest achievements,
          best qualities and skills.
        </p>
      </div>
      <ckeditor v-model="editorData" :config="editorConfig"></ckeditor>
    </div>

    <!-- EMPLOYEMENT HISTORY -->
    <div class="px-10 pt-10 space-y-2">
      <div>
        <h3 class="font-bold text-xl">Employement History</h3>
        <p class="text-gray-400 text-sm">
          Show your relevant experience (last 10 years). Use bullet points to
          note your achievements, if possible - use numbers/facts (Achieved X,
          measured by Y, by doing Z)
        </p>
      </div>
      <div class="space-y-2">
        <div v-for="(i, index) in form.employeeHistory" :key="index">
          <AccordionDefault>
            <template v-slot:title>
              <div class="px-2 flex flex-col items-start">
                <span class="font-semibold text-sm"
                  >{{ i.job ?? '(Not specified)' }}
                  {{ i.employer ? 'at ' + i.employer : '' }}</span
                >
                <span class="text-gray-400 text-sm">
                  {{
                    i.start ? i.start.month + ' ' + i.start.year + ' - ' : ''
                  }}
                  {{ i.end ? i.end.month + ' ' + i.end.year : '' }}</span
                >
              </div>
            </template>
            <template v-slot:content>
              <div class="px-2 space-y-3">
                <div class="space-x-6 w-full flex flex-row justify-center">
                  <div class="flex flex-col space-y-2 w-1/2">
                    <div class="flex flex-row space-x-2 items-center">
                      <label class="text-gray-400 text-sm">Job Title</label>
                    </div>
                    <div>
                      <InputText v-model="i.job" required />
                    </div>
                  </div>
                  <div class="flex flex-col space-y-2 w-1/2">
                    <div class="flex flex-row space-x-2 items-center">
                      <label class="text-gray-400 text-sm">Employer</label>
                    </div>
                    <div>
                      <InputText v-model="i.employer" required />
                    </div>
                  </div>
                </div>

                <div class="space-x-6 w-full flex flex-row justify-center">
                  <div class="w-1/2 flex-col flex space-y-2">
                    <div class="flex flex-row space-x-2 items-center">
                      <label class="text-gray-400 text-sm"
                        >Start & End Date</label
                      >
                      <TooltipsDefault text="Mulai dan Terakhir bekerja" />
                    </div>
                    <div class="flex flex-row space-x-2 w-full justify-center">
                      <div class="w-1/2">
                        <month-picker-input
                          no-default
                          date-format="%n / %Y"
                          v-model="i.start"
                        ></month-picker-input>
                      </div>
                      <div class="w-1/2">
                        <month-picker-input
                          no-default
                          date-format="%n / %Y"
                          v-model="i.end"
                        ></month-picker-input>
                      </div>
                    </div>
                  </div>
                  <div class="w-1/2 flex-col flex space-y-2">
                    <div class="flex flex-row space-x-2 items-center">
                      <label class="text-gray-400 text-sm">City</label>
                    </div>
                    <div>
                      <InputSelect
                        v-model="i.city"
                        :resources="cities"
                        required
                      />
                    </div>
                  </div>
                </div>

                <div class="space-x-6 w-full flex flex-row justify-center">
                  <div class="flex flex-col space-y-2 w-full">
                    <div class="flex flex-row space-x-2 items-center">
                      <label class="text-gray-400 text-sm">Description</label>
                    </div>
                    <div>
                      <InputText v-model="i.descrption" required />
                    </div>
                  </div>
                </div>
              </div>
            </template>
          </AccordionDefault>
        </div>
        <button
          @click="addEmployeeHistory"
          class="text-sm font-semibold text-blue-600 hover:text-blue-800"
        >
          + Add employee
        </button>
      </div>
    </div>

    <!-- EDUCATION -->
    <div class="px-10 pt-10 space-y-2">
      <div>
        <h3 class="font-bold text-xl">Education</h3>
        <p class="text-gray-400 text-sm">
          A varied education on your resume sums up the value that your
          learnings and background will bring to job.
        </p>
      </div>
      <div class="space-y-2">
        <div v-for="(i, index) in form.education" :key="index">
          <AccordionDefault>
            <template v-slot:title>
              <div class="px-2 flex flex-col items-start">
                <span class="font-semibold text-sm"
                  >{{ i.degree ?? '(Not specified)' }}
                  {{ i.degree ? 'at ' + i.school : '' }}</span
                >
                <span class="text-gray-400 text-sm"
                  >{{
                    i.start ? i.start.month + ' ' + i.start.year + ' - ' : ''
                  }}
                  {{ i.end ? i.end.month + ' ' + i.end.year : '' }}</span
                >
              </div>
            </template>
            <template v-slot:content>
              <div class="px-2 space-y-3">
                <div class="space-x-6 w-full flex flex-row justify-center">
                  <div class="flex flex-col space-y-2 w-1/2">
                    <div class="flex flex-row space-x-2 items-center">
                      <label class="text-gray-400 text-sm">School</label>
                    </div>
                    <div>
                      <InputText v-model="i.school" required />
                    </div>
                  </div>
                  <div class="flex flex-col space-y-2 w-1/2">
                    <div class="flex flex-row space-x-2 items-center">
                      <label class="text-gray-400 text-sm">Degree</label>
                    </div>
                    <div>
                      <InputText v-model="i.degree" required />
                    </div>
                  </div>
                </div>

                <div class="space-x-6 w-full flex flex-row justify-center">
                  <div class="w-1/2 flex-col flex space-y-2">
                    <div class="flex flex-row space-x-2 items-center">
                      <label class="text-gray-400 text-sm"
                        >Start & End Date</label
                      >
                      <TooltipsDefault text="Mulai dan Terakhir bekerja" />
                    </div>
                    <div class="flex flex-row space-x-2 w-full justify-center">
                      <div class="w-1/2">
                        <month-picker-input
                          no-default
                          date-format="%n / %Y"
                          v-model="i.start"
                        ></month-picker-input>
                      </div>
                      <div class="w-1/2">
                        <month-picker-input
                          no-default
                          date-format="%n / %Y"
                          v-model="i.end"
                        ></month-picker-input>
                      </div>
                    </div>
                  </div>
                  <div class="w-1/2 flex-col flex space-y-2">
                    <div class="flex flex-row space-x-2 items-center">
                      <label class="text-gray-400 text-sm">City</label>
                    </div>
                    <div>
                      <InputSelect
                        v-model="i.city"
                        :resources="cities"
                        required
                      />
                    </div>
                  </div>
                </div>

                <div class="space-x-6 w-full flex flex-row justify-center">
                  <div class="flex flex-col space-y-2 w-full">
                    <div class="flex flex-row space-x-2 items-center">
                      <label class="text-gray-400 text-sm">Description</label>
                    </div>
                    <div>
                      <InputText v-model="i.descrption" required />
                    </div>
                  </div>
                </div>
              </div>
            </template>
          </AccordionDefault>
        </div>
        <button
          @click="addEducation"
          class="text-sm font-semibold text-blue-600 hover:text-blue-800"
        >
          + Add Education
        </button>
      </div>
    </div>

    <!-- Skills -->
    <div class="px-10 pt-10 space-y-2">
      <div>
        <h3 class="font-bold text-xl">Skills</h3>
        <p class="text-gray-400 text-sm">
          Choose 5 of the most important skills to show your talents! Make sure
          they match the keywords of the job listing if applying via an online
          system
        </p>
      </div>
      <div class="flex flex-row flex-wrap gap-2">
        <div v-for="(i, index) in skills" :key="i.id">
          <ChipDefault
            :name="i.name"
            :selected="i.selected"
            @onClick="addSkill(i, index)"
          />
        </div>
      </div>
      <div class="space-y-2 pt-6">
        <div v-for="(i, index) in form.skillSelected" :key="index">
          <AccordionDefault>
            <template v-slot:title>
              <div class="px-2 flex flex-col items-start">
                <span class="font-semibold text-sm">{{ i.name }}</span>
                <span class="text-gray-400 text-sm">{{ i.level }}</span>
              </div>
            </template>
            <template v-slot:content>
              <div class="px-2 space-y-3">
                <div class="space-x-6 w-full flex flex-row justify-center">
                  <div class="flex flex-col space-y-2 w-1/2">
                    <div class="flex flex-row space-x-2 items-center">
                      <label class="text-gray-400 text-sm">Skill</label>
                    </div>
                    <div>
                      <InputText
                        v-model="i.name"
                        :disabled="i.id !== null"
                        required
                      />
                    </div>
                  </div>
                  <div class="flex flex-col space-y-2 w-1/2">
                    <div class="flex flex-row space-x-2 items-center">
                      <label class="text-gray-400 text-sm">Level</label>
                    </div>
                    <div>
                      <!-- <InputSelect :resources="levels" v-model="i.level" /> -->
                      <div class="flex flex-row">
                        <div
                          class="focus:ring-1 text-sm focus:bg-white w-full focus:shadow-xl hover:ring-1 border px-3 py-[18px] focus:outline-none bg-gray-100"
                          @click="i.level = 'Low'"
                          :class="{
                            'bg-red-400': i.level === 'Low',
                          }"
                        ></div>
                        <div
                          class="focus:ring-1 text-sm focus:bg-white w-full focus:shadow-xl hover:ring-1 border px-3 py-[18px] focus:outline-none bg-gray-100"
                          @click="i.level = 'Skillful'"
                          :class="{
                            'bg-yellow-500': i.level === 'Skillful',
                          }"
                        ></div>
                        <div
                          class="focus:ring-1 text-sm focus:bg-white w-full focus:shadow-xl hover:ring-1 border px-3 py-[18px] focus:outline-none bg-gray-100"
                          @click="i.level = 'Experienced'"
                          :class="{
                            'bg-green-500': i.level === 'Experienced',
                          }"
                        ></div>
                        <div
                          class="focus:ring-1 text-sm focus:bg-white w-full focus:shadow-xl hover:ring-1 border px-3 py-[18px] focus:outline-none bg-gray-100"
                          @click="i.level = 'Expert'"
                          :class="{
                            'bg-purple-400': i.level === 'Expert',
                          }"
                        ></div>
                      </div>
                    </div>
                  </div>
                </div>
              </div>
            </template>
          </AccordionDefault>
        </div>
        <button
          @click="addMoreSkill"
          class="text-sm font-semibold text-blue-600 hover:text-blue-800"
        >
          + Add one more skill
        </button>
      </div>
    </div>

    <div class="px-10 pt-10 flex justify-end">
      <button
        class="bg-green-600 rounded-lg text-white text-sm px-3 py-2"
        @click="showLog"
      >
        Submit
      </button>
    </div>
  </div>
</template>

<style>
.month-picker-input {
  @apply bg-gray-100 p-2 rounded-none w-full !important;
}
.month-picker-input-container {
  @apply w-full min-w-0 !important;
}
</style>

<script>
export default {
  name: 'IndexPage',
  data() {
    return {
      editorData: '<p>Content of the editor.asdasdasd</p>',
      editorConfig: {
        // The configuration of the editor.
      },
      skillColor: 'low',
      skills: [
        {
          id: 1,
          selected: false,
          name: 'Java',
        },
        {
          id: 2,
          selected: false,
          name: 'JavaScript',
        },
        {
          id: 3,
          selected: false,
          name: 'Python',
        },
        {
          id: 4,
          selected: false,
          name: 'Git',
        },
        {
          id: 5,
          selected: false,
          name: 'SQL',
        },
        {
          id: 6,
          selected: false,
          name: 'C++',
        },
        {
          id: 7,
          selected: false,
          name: 'TypeScript',
        },
        {
          id: 8,
          selected: false,
          name: 'C#',
        },
        {
          id: 9,
          selected: false,
          name: 'Docker',
        },
        {
          id: 10,
          selected: false,
          name: 'PHP',
        },
        {
          id: 11,
          selected: false,
          name: 'React',
        },
        {
          id: 12,
          selected: false,
          name: 'MongoDB',
        },
        {
          id: 13,
          selected: false,
          name: 'Toad',
        },
        {
          id: 14,
          selected: false,
          name: 'HTML CSS 3',
        },
        {
          id: 15,
          selected: false,
          name: 'MS SQL Server',
        },
      ],
      countries: [
        {
          id: 1,
          name: 'Indonesia',
        },
        {
          id: 2,
          name: 'Malaysia',
        },
        {
          id: 3,
          name: 'Singapore',
        },
      ],
      cities: [
        {
          id: 1,
          name: 'Jakarta',
        },
        {
          id: 2,
          name: 'Bandung',
        },
        {
          id: 3,
          name: 'Bali',
        },
        {
          id: 4,
          name: 'Yogyakarta',
        },
      ],
      form: {
        jobTitle: null,
        photo: null,
        firstName: null,
        lastName: null,
        email: null,
        phone: null,
        country: null,
        city: null,
        address: null,
        postalCode: null,
        drivingLicense: null,
        nationality: null,
        placeOfBirth: null,
        dateOfBirth: null,
        description: null,
        employeeHistory: [],
        education: [],
        skillSelected: [],
      },
      validate: {
        photo: false,
      },
    }
  },
  watch: {
    'form.employeeHistory'(val) {
      console.log(val)
    },
  },
  methods: {
    colorSkill(val) {
      switch (val) {
        case 'low':
          this.skillColor = 'low'
          break

        case 'skillful':
          console.log('skilful')
          break

        default:
          console.log('asd')
      }
    },
    getExtension(filename) {
      const parts = filename.split('/')
      return parts
      // return parts[parts.length - 1];
    },

    uploadPhoto(e) {
      const file = e.target.files
      const ext = this.getExtension(file[0].type)

      if (ext[0] !== 'image') {
        this.validate.photo = true
        this.form.photo = null
      } else {
        this.validate.photo = false
        this.form.photo = file[0]
      }

      // console.log(file[0].type)
    },
    addEmployeeHistory() {
      this.form.employeeHistory.push({
        job: null,
        employer: null,
        start: null,
        end: null,
        city: null,
        description: null,
      })
    },
    addEducation() {
      this.form.education.push({
        school: null,
        degree: null,
        start: null,
        end: null,
        city: null,
        description: null,
      })
    },
    addSkill(skill, index) {
      this.skills[index].selected = !this.skills[index].selected

      if (this.skills[index].selected) {
        this.form.skillSelected.push({
          id: skill.id,
          level: 'Low',
          name: skill.name,
        })
      } else {
        this.form.skillSelected.forEach((value, ind) => {
          if (value.id === skill.id) {
            this.$delete(this.form.skillSelected, ind)
          }
        })
      }
    },
    addMoreSkill() {
      this.form.skillSelected.push({
        id: null,
        level: 'Low',
        name: null,
      })
    },
    showLog() {
      console.log(this.form)
    },
  },
}
</script>
