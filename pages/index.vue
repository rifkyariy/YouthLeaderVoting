<template>
  <div>
    <div class="bg-gray-50 h-screen flex content-center">
      <!-- Intro -->
      <div
        v-if="step == 0"
        id="preambule"
        class="w-full py-12 px-6 sm:px-6 lg:py-16 lg:px-8 my-auto"
      >
        <h1 class="text-6xl">🗳</h1>
        <div class="head">
          <h2
            class="
              py-6
              text-3xl
              font-extrabold
              tracking-tight
              text-gray-900
              sm:text-4xl
            "
          >
            <span class="block text-indigo-600">#timetovote.</span>
            <span class="block">Dah Siap Milih?</span>
          </h2>
        </div>
        <div class="py-2">
          <label
            for="first-name"
            class="block text-sm font-medium text-gray-700"
            >Boleh kenalan dulu nama kamu siapa ?
          </label>
          <input
            id="first-name"
            v-model="userVote"
            type="text"
            autocomplete="given-name"
            class="
              mt-4
              focus:ring-indigo-600 focus:border-indigo-600
              block
              w-full
              shadow-sm
              sm:text-sm
              border-gray-300
              rounded-md
              p-2
            "
            autofocus
          />
        </div>

        <!-- Button -->
        <div class="mt-3 flex lg:mt-0 lg:flex-shrink-0 flex-row-reverse">
          <div class="inline-flex rounded-md shadow">
            <a
              href="#"
              class="
                inline-flex
                items-center
                justify-center
                px-5
                py-3
                border border-transparent
                text-base
                font-medium
                rounded-md
                text-white
                bg-indigo-600
                hover:bg-indigo-700
              "
              @click="validateUser"
            >
              Dah Lanjut 👉
            </a>
          </div>
        </div>
      </div>

      <!-- Voting -->
      <div
        v-if="step == 1"
        id="vote"
        class="w-full py-12 px-6 sm:px-6 lg:py-16 lg:px-8 my-auto"
      >
        <h1 class="text-6xl">🗳</h1>
        <div class="head">
          <h2
            class="
              pt-6
              pb-3
              text-3xl
              font-extrabold
              tracking-tight
              text-gray-900
              sm:text-4xl
            "
          >
            <span class="block text-indigo-600">Candidate.</span>
            <span class="block">Sok atuh dipilih</span>
          </h2>
        </div>
        <div class="py-0">
          <div
            id="tabs-1-panel-1"
            class="py-4 space-y-10"
            aria-labelledby="tabs-1-tab-1"
            role="tabpanel"
            tabindex="0"
          >
            <div class="grid grid-cols-2 gap-x-4">
              <div
                v-for="candidate in listCandidate"
                :key="candidate.id"
                class="group relative text-sm"
                @click="voteCandidateId = candidate.id"
              >
                <span
                  class="text-xs font-extrabold tracking-tight text-transparent"
                  :class="{
                    'text-indigo-500': voteCandidateId == candidate.id,
                  }"
                  >✅ Dipilih</span
                >
                <div
                  class="
                    mt-1
                    aspect-w-1 aspect-h-1
                    rounded-lg
                    bg-gray-100
                    overflow-hidden
                    group-hover:opacity-75
                    border-4
                  "
                  :class="{
                    'border-indigo-500': voteCandidateId == candidate.id,
                  }"
                >
                  <img
                    :src="candidate.avatar"
                    alt="Models sitting back to back, wearing Basic Tee in black and bone."
                    class="object-center object-fill"
                  />
                </div>
                <a class="mt-3 block font-extrabold text-gray-900">
                  <span class="absolute z-10 inset-0" aria-hidden="true"></span>
                  {{ candidate.name }}
                </a>
                <p aria-hidden="true" class="mt-1">
                  Kandidat No {{ candidate.id }}
                </p>
              </div>
            </div>
          </div>
        </div>
        <!-- Button -->
        <div
          class="
            mt-3
            flex
            lg:mt-0 lg:flex-shrink-0
            flex-row-reverse
            justify-between
          "
        >
          <div class="inline-flex rounded-md shadow mx-1">
            <a
              href="#"
              class="
                inline-flex
                items-center
                justify-center
                px-5
                py-3
                border border-transparent
                text-base
                font-medium
                rounded-md
                text-white
                bg-indigo-600
                hover:bg-indigo-700
              "
              @click="validateVote()"
            >
              Oke Sip 👌
            </a>
          </div>
          <div class="inline-flex rounded-md shadow mx-1">
            <a
              href="#"
              class="
                inline-flex
                items-center
                justify-center
                px-5
                py-3
                border border-transparent
                text-base
                font-medium
                rounded-md
                text-indigo-600
                bg-white
                hover:bg-indigo-50
              "
              @click="step = 0"
            >
              👈 Kembali
            </a>
          </div>
        </div>
      </div>

      <!-- Alert -->
    </div>
  </div>
</template>

<script>
import axios from 'axios'
const baseURL = 'https://62dee1f29c47ff309e7df07d.mockapi.io'

export default {
  data() {
    return {
      step: 0,
      userVote: '',
      voteCandidateId: '',
      listCandidate: [],
    }
  },
  mounted() {
    axios(`${baseURL}/LeaderCandidate`, {
      crossDomain: true,
    }).then(({ data }) => {
      this.listCandidate = data
    })
  },
  methods: {
    validateUser() {
      if (this.userVote === '') {
        this.$swal({
          icon: 'error',
          title: 'Oopsiee...',
          text: 'Nama ndak boleh kosong!',
          confirmButtonText: 'Baiqlah 👍',
        })
      } else {
        this.step = 1
      }
    },
    validateVote() {
      if (this.userVote === '') {
        this.$swal({
          icon: 'error',
          title: 'Oopsiee...',
          text: 'Nama ndak boleh kosong!',
          confirmButtonText: 'Baiqlah 👍',
        })
      } else if (this.voteCandidateId === '' || this.voteCandidateId == null) {
        this.$swal({
          icon: 'error',
          title: 'Oopsiee...',
          text: 'Pilih kandidat dulu gan!',
          confirmButtonText: 'Baiqlah 👍',
        })
      } else {
        this.$swal({
          icon: 'warning',
          title: 'Dah Yakin ?',
          text: 'Nanti dah gak bisa ganti lho',
          confirmButtonText: 'Mengerti 👍',
          showCancelButton: true,
          reverseButtons: true,
        }).then((result) => {
          if (result.isConfirmed) {
            this.sendVoteData(this.userVote, this.voteCandidateId)
            this.$swal({
              imageWidth: '30%',
              imageUrl:
                'data:image/svg+xml;base64,PD94bWwgdmVyc2lvbj0iMS4wIiBlbmNvZGluZz0idXRmLTgiPz4KPHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIiBzdHlsZT0ibWFyZ2luOiBhdXRvOyBiYWNrZ3JvdW5kOiByZ2IoMjU1LCAyNTUsIDI1NSkgbm9uZSByZXBlYXQgc2Nyb2xsIDAlIDAlOyBkaXNwbGF5OiBibG9jazsgc2hhcGUtcmVuZGVyaW5nOiBhdXRvOyIgd2lkdGg9IjIwMHB4IiBoZWlnaHQ9IjIwMHB4IiB2aWV3Qm94PSIwIDAgMTAwIDEwMCIgcHJlc2VydmVBc3BlY3RSYXRpbz0ieE1pZFlNaWQiPgo8ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSg1MCw1MCkiPgogIDxnIHRyYW5zZm9ybT0ic2NhbGUoMC43KSI+CiAgPGNpcmNsZSBjeD0iMCIgY3k9IjAiIHI9IjUwIiBmaWxsPSIjNDUwOTg4Ij48L2NpcmNsZT4KICA8Y2lyY2xlIGN4PSIwIiBjeT0iLTI4IiByPSIxNSIgZmlsbD0iI2ZmZmZmZiI+CiAgICA8YW5pbWF0ZVRyYW5zZm9ybSBhdHRyaWJ1dGVOYW1lPSJ0cmFuc2Zvcm0iIHR5cGU9InJvdGF0ZSIgZHVyPSIxcyIgcmVwZWF0Q291bnQ9ImluZGVmaW5pdGUiIGtleVRpbWVzPSIwOzEiIHZhbHVlcz0iMCAwIDA7MzYwIDAgMCI+PC9hbmltYXRlVHJhbnNmb3JtPgogIDwvY2lyY2xlPgogIDwvZz4KPC9nPgo8IS0tIFtsZGlvXSBnZW5lcmF0ZWQgYnkgaHR0cHM6Ly9sb2FkaW5nLmlvLyAtLT48L3N2Zz4=',
              title: 'Mengirim 🚀',
              allowOutsideClick: false,
              showConfirmButton: false,
            })
          }
        })
      }
    },
    sendVoteData(user, voteCandidateId) {
      axios
        .post(`${baseURL}/LeaderCandidate/${voteCandidateId}/UserVote`, {
          Username: user,
        })
        .then((response) => {
          if (response.status === 201) {
            this.$swal({
              icon: 'success',
              title: 'Mashook',
              text: 'Berhasil Berhasil Horee',
              confirmButtonText: 'Mengokee 👍',
            }).then((result) => {
              if (result.isConfirmed) {
                this.$router.go()
              }
            })
          }
        })
    },
  },
}
</script>
