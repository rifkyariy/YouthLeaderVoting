<template>
  <div>
    <div class="bg-gray-50 h-screen flex content-center">
      <!-- This example requires Tailwind CSS v2.0+ -->
      <div class="py-12 bg-white w-full">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
          <div class="lg:text-center">
            <a href="/">
              <h2
                class="
                  text-base text-indigo-600
                  font-semibold
                  tracking-wide
                  uppercase
                "
              >
                #timetovote
              </h2>
            </a>
            <p
              class="
                mt-2
                text-3xl
                leading-8
                font-extrabold
                tracking-tight
                text-gray-900
                sm:text-4xl
              "
            >
              Vote Recap
            </p>
            <p class="mt-4 max-w-2xl text-xl text-gray-500 lg:mx-auto">
              Lorem ipsum dolor sit amet consect adipisicing elit. Possimus
              magnam voluptatum cupiditate veritatis in accusamus quisquam.
            </p>
          </div>

          <div v-if="loading.mostVote" class="flex justify-center pt-2">
            <div class="text-center">
              <img
                src="data:image/svg+xml;base64,PD94bWwgdmVyc2lvbj0iMS4wIiBlbmNvZGluZz0idXRmLTgiPz4KPHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIiBzdHlsZT0ibWFyZ2luOiBhdXRvOyBiYWNrZ3JvdW5kOiByZ2IoMjU1LCAyNTUsIDI1NSkgbm9uZSByZXBlYXQgc2Nyb2xsIDAlIDAlOyBkaXNwbGF5OiBibG9jazsgc2hhcGUtcmVuZGVyaW5nOiBhdXRvOyIgd2lkdGg9IjIwMHB4IiBoZWlnaHQ9IjIwMHB4IiB2aWV3Qm94PSIwIDAgMTAwIDEwMCIgcHJlc2VydmVBc3BlY3RSYXRpbz0ieE1pZFlNaWQiPgo8ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSg1MCw1MCkiPgogIDxnIHRyYW5zZm9ybT0ic2NhbGUoMC43KSI+CiAgPGNpcmNsZSBjeD0iMCIgY3k9IjAiIHI9IjUwIiBmaWxsPSIjNDUwOTg4Ij48L2NpcmNsZT4KICA8Y2lyY2xlIGN4PSIwIiBjeT0iLTI4IiByPSIxNSIgZmlsbD0iI2ZmZmZmZiI+CiAgICA8YW5pbWF0ZVRyYW5zZm9ybSBhdHRyaWJ1dGVOYW1lPSJ0cmFuc2Zvcm0iIHR5cGU9InJvdGF0ZSIgZHVyPSIxcyIgcmVwZWF0Q291bnQ9ImluZGVmaW5pdGUiIGtleVRpbWVzPSIwOzEiIHZhbHVlcz0iMCAwIDA7MzYwIDAgMCI+PC9hbmltYXRlVHJhbnNmb3JtPgogIDwvY2lyY2xlPgogIDwvZz4KPC9nPgo8IS0tIFtsZGlvXSBnZW5lcmF0ZWQgYnkgaHR0cHM6Ly9sb2FkaW5nLmlvLyAtLT48L3N2Zz4="
                alt=""
                srcset=""
              />
              <h2 class="font-semibold tracking-wide text-indigo-800 -mt-2">
                Sedang Memuat Data
              </h2>
            </div>
          </div>

          <div v-if="!loading.mostVote" class="mt-10 px-24 grid grid-cols-2">
            <dl class="w-full">
              <div>
                <h1 class="text-xl font-extrabold tracking-tight text-gray-900">
                  🗿 Grafik
                </h1>
                <Pie :chart-options="chartOptions" :chart-data="chartData" />
              </div>
            </dl>
            <dl class="space-y-8 pl-8">
              <h1 class="text-xl font-extrabold tracking-tight text-gray-900">
                🤔 Ingfo Lain
              </h1>
              <div class="relative">
                <dt>
                  <div
                    class="
                      absolute
                      flex
                      items-center
                      justify-center
                      h-12
                      w-12
                      rounded-md
                      bg-indigo-500
                      text-white
                    "
                  >
                    <!-- Heroicon name: outline/globe-alt -->
                    <h1 class="text-3xl">👑</h1>
                  </div>
                  <p class="ml-16 text-xl leading-6 font-bold text-gray-900">
                    {{ loading.mostVote ? '-' : mostVote }}
                  </p>
                  <p class="ml-16 text-xs leading-6 font-medium text-gray-500">
                    Suara Terbanyak
                  </p>
                </dt>
              </div>

              <div class="relative">
                <dt>
                  <div
                    class="
                      absolute
                      flex
                      items-center
                      justify-center
                      h-12
                      w-12
                      rounded-md
                      bg-indigo-500
                      text-white
                    "
                  >
                    <!-- Heroicon name: outline/scale -->
                    <h1 class="text-3xl">🤯</h1>
                  </div>
                  <p class="ml-16 text-xl leading-6 font-bold text-gray-900">
                    {{ mostVoteScore }}
                    <span class="text-sm leading-6 font-bold text-gray-300">
                      vs {{ leastVoteScore }}
                    </span>
                  </p>
                  <p class="ml-16 text-xs leading-6 font-medium text-gray-500">
                    Unggul Suara
                  </p>
                </dt>
              </div>

              <div class="relative">
                <dt>
                  <div
                    class="
                      absolute
                      flex
                      items-center
                      justify-center
                      h-12
                      w-12
                      rounded-md
                      bg-indigo-500
                      text-white
                    "
                  >
                    <!-- Heroicon name: outline/scale -->
                    <h1 class="text-3xl">👨‍👩‍👦‍👦</h1>
                  </div>
                  <p class="ml-16 text-xl leading-6 font-bold text-gray-900">
                    {{ totalVoteScore }}
                  </p>
                  <p class="ml-16 text-xs leading-6 font-medium text-gray-500">
                    Total Suara Masuk
                  </p>
                </dt>
              </div>
            </dl>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import { Pie } from 'vue-chartjs'

import {
  Chart as ChartJS,
  Title,
  Tooltip,
  Legend,
  ArcElement,
  CategoryScale,
} from 'chart.js'

ChartJS.register(Title, Tooltip, Legend, ArcElement, CategoryScale)

const baseURL = 'https://62dee1f29c47ff309e7df07d.mockapi.io'

export default {
  components: {
    Pie,
  },
  data() {
    return {
      chartBlueprint: {
        labels: [],
        datasets: [
          {
            data: [],
            backgroundColor: ['#6466E9', '#F2AE47'],
          },
        ],
      },
      chartData: {},
      chartOptions: {
        responsive: true,
        plugins: {
          legend: {
            display: true,
            position: 'bottom',
          },
        },
      },
      listCandidate: [],
      loading: {
        mostVote: false,
      },
      mostVote: '-',
      mostVoteScore: 0,
      leastVoteScore: 0,
      totalVoteScore: 0,
    }
  },
  mounted() {
    this.$nextTick(
      async function () {
        this.$set(this.loading, 'mostVote', true)
        const data = await this.fetchCandidate()
        this.listCandidate = data

        // loop based on candidate id
        for (let i = 0; i < data.length; i++) {
          await this.fetchDetailCandidate(data, i)
        }

        // change state of chart data to API data
        this.chartData = this.chartBlueprint
        this.$set(this.loading, 'mostVote', false)
      }.bind(this)
    )
  },
  methods: {
    fetchCandidate() {
      return new Promise((resolve, reject) => {
        axios(`${baseURL}/LeaderCandidate`, {
          crossDomain: true,
        })
          .then(({ data }) => {
            resolve(data)
          })
          .catch((err) => reject(err))
      })
    },
    async fetchDetailCandidate(listCandidateData, i) {
      this.chartBlueprint.labels.unshift(listCandidateData[i].name)

      // Get from API user vote based on candidate id
      await axios(
        `${baseURL}/LeaderCandidate/${listCandidateData[i].id}/UserVote`,
        {
          crossDomain: true,
        }
      ).then(({ data }) => {
        // adding data into chartdata blueprint
        this.chartBlueprint.datasets[0].data.unshift(data.length)
        this.totalVoteScore += data.length

        this.checkMostVote(i, data.length)

        // Sum total vote data
        // this.totalVoteScore = total
      })
    },
    // check
    checkMostVote(index, candidateScore) {
      if (this.mostVote === '-') {
        this.mostVote = this.listCandidate.at(index).name
        this.mostVoteScore = candidateScore
      } else if (candidateScore > this.mostVoteScore) {
        this.mostVote = this.listCandidate.at(index).name
        this.mostVoteScore = candidateScore
      }

      if (this.leastVoteScore === 0) {
        this.leastVoteScore = candidateScore
      } else if (candidateScore < this.leastVoteScore) {
        this.leastVoteScore = candidateScore
      }
    },
  },
}
</script>

<style>
</style>