<template>
  <div>
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

    PROFESSIONAL SUMMARY
  </div>
</template>

<script>
export default {
  name: 'IndexPage',
  data() {
    return {
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
      },
    }
  },
}
</script>
