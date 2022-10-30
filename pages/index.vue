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
            <InputText required />
          </div>
        </div>
        <div class="flex flex-col space-y-2 w-1/2">
          <div class="w-full h-full flex items-end">
            <div
              class="h-3/4 bg-gray-300 w-16 rounded flex items-center justify-center"
            >
              <img src="~/assets/svg/user.svg" class="w-8 h-8" />
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
            <InputText required />
          </div>
        </div>
        <div class="flex flex-col space-y-2 w-1/2">
          <div class="pt-4 flex flex-row space-x-2 items-center">
            <label class="text-gray-400 text-sm">Last Name</label>
          </div>
          <div>
            <InputText required />
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
            <InputText required />
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
              <div class="p-2 flex flex-col items-start">
                <span class="font-semibold text-sm">{{
                  i.job ?? '(Not specified)'
                }}</span>
                <span class="text-gray-400 text-sm">Jul 2022 - Jul 2030</span>
              </div>
            </template>
            <template v-slot:content>
              <div class="px-4 space-y-3">
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
                      <div>
                        <InputText
                          placeholder="MM / YYYY"
                          v-model="i.start"
                          required
                        />
                      </div>
                      <div>
                        <InputText
                          placeholder="MM / YYYY"
                          v-model="i.end"
                          required
                        />
                      </div>
                    </div>
                  </div>
                  <div class="w-1/2 flex-col flex space-y-2">
                    <div class="flex flex-row space-x-2 items-center">
                      <label class="text-gray-400 text-sm">City</label>
                    </div>
                    <div>
                      <InputSelect :resources="cities" required />
                    </div>
                  </div>
                </div>

                <div class="space-x-6 w-full flex flex-row justify-center">
                  <div class="flex flex-col space-y-2 w-1/2">
                    <div class="flex flex-row space-x-2 items-center">
                      <label class="text-gray-400 text-sm">Description</label>
                    </div>
                    <div>
                      <InputText v-model="i.descrption" required />
                    </div>
                  </div>
                  <div class="flex flex-col space-y-2 w-1/2">
                    <div class="flex flex-row space-x-2 items-center">
                      <label class="text-gray-400 text-sm">Employer</label>
                    </div>
                    <div>
                      <InputText v-model="i.description" required />
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
  </div>
</template>

<script>
export default {
  name: 'IndexPage',
  data() {
    return {
      editorData: '<p>Content of the editor.asdasdasd</p>',
      editorConfig: {
        // The configuration of the editor.
      },

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
        country: null,
        city: null,
        employeeHistory: [],
      },
    }
  },

  methods: {
    addEmployeeHistory() {
      this.form.employeeHistory.push({
        job: null,
        employer: null,
        start: null,
        end: null,
        description: null,
      })
    },
  },
}
</script>
