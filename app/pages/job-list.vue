<template>
  <div class="bg-white w-[100%] mt-[100px]">
    <div class="flex flex-wrap items-center bg-white p-1 rounded-xl border border-gray-200 shadow-sm w-full max-w-[1400px] mx-auto font-sans relative">
      <div class="flex flex-1 items-center gap-2 px-4 min-h-[56px] min-w-[300px]">
        <svg class="w-5 h-5 text-gray-400 shrink-0" fill="none" stroke="currentColor" viewBox="0 0 24 24">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z" />
        </svg>
        <div class="flex flex-wrap gap-2">
          <input type="text" placeholder="Add more..." class="outline-none text-sm text-gray-500 bg-transparent flex-1 min-w-[50px]" />
        </div>
        <div class="h-8 w-[1px] bg-gray-200 ml-auto hidden md:block"></div>
      </div>

      <div v-for="(dropdown, index) in dropdownConfigs" :key="index" class="relative group">
        <div @click="toggleDropdown(dropdown.key)" class="flex items-center gap-2 px-6 border-r border-gray-100 h-14 cursor-pointer hover:bg-gray-50 transition-colors">
          <svg v-html="dropdown.icon" class="w-5 h-5 text-gray-400" fill="none" stroke="currentColor" viewBox="0 0 24 24" stroke-width="2"></svg>
          <span class="text-sm font-medium whitespace-nowrap" :class="selections[dropdown.key] ? 'text-gray-900' : 'text-gray-500'">
            {{ selections[dropdown.key] || dropdown.label }}
          </span>
          <svg class="w-4 h-4 text-gray-400 transition-transform" :class="{'rotate-180': openDropdown === dropdown.key}" fill="currentColor" viewBox="0 0 20 20">
            <path d="M5.293 7.293a1 1 0 011.414 0L10 10.586l3.293-3.293a1 1 0 111.414 1.414l-4 4a1 1 0 01-1.414 0l-4-4a1 1 0 010-1.414z"/>
          </svg>
        </div>

        <div v-if="openDropdown === dropdown.key" class="absolute top-full left-0 w-64 bg-white border border-gray-200 rounded-xl shadow-xl z-50 mt-2 py-2 max-h-60 overflow-y-auto">
          <button v-for="option in dropdown.options" :key="option" @click="selectOption(dropdown.key, option)" class="w-full text-left px-4 py-2.5 text-sm hover:bg-blue-50 hover:text-blue-600 transition-colors">
            {{ option }}
          </button>
        </div>
      </div>

      <button class="bg-blue-500 text-white px-8 h-12 rounded-lg text-sm font-bold tracking-tight hover:bg-gray-800 transition-all uppercase m-1 ml-4">
        Start Searching
      </button>
    </div>

    <div class="bg-white min-h-screen w-[100%] p-8">
      <div class="max-w-8xl mx-auto flex gap-8">
        <aside class="w-64 shrink-0 hidden lg:block">
          <h2 class="text-xl font-bold mb-6">Filters</h2>
          
          <div class="mb-8">
            <p class="text-gray-400 text-sm font-bold uppercase mb-4 tracking-wider">Type of Employment</p>
            <div class="space-y-3">
              <label v-for="item in scheduleOptions" :key="item" class="flex items-center gap-3 cursor-pointer group">
                <input type="checkbox" class="w-5 h-5 rounded accent-black cursor-pointer border-gray-300">
                <span class="text-gray-700 font-medium text-sm group-hover:text-blue-500 transition-colors">{{ item }}</span>
              </label>
            </div>
          </div>

        <div class="mb-8">
            <p class="text-gray-400 text-sm font-bold uppercase mb-4 tracking-wider">Employment type</p>
            <div class="space-y-3">
                <label v-for="item in employmentType" :key="item" class="flex items-center gap-3 cursor-pointer group">
                <input type="checkbox" class="w-5 h-5 rounded accent-black cursor-pointer border-gray-300">
                <span class="text-gray-700 font-medium text-sm group-hover:text-blue-500 transition-colors">{{ item }}</span>
                </label>
            </div>
        </div>

        <div class="mb-8">
        <p class="text-gray-400 text-sm font-bold uppercase mb-4 tracking-wider">Seniority Level</p>
        <div class="space-y-3">
            <label v-for="level in senioritylevel" :key="level" class="flex items-center gap-3 cursor-pointer group">
            <input type="checkbox" class="w-5 h-5 rounded accent-black cursor-pointer border-gray-300">
            <span class="text-gray-700 font-medium text-sm group-hover:text-blue-500 transition-colors">{{ level }}</span>
            </label>
        </div>
        </div>
        </aside>

        <main class="flex-1">
          <div class="flex justify-between items-center mb-8">
            <h1 class="text-3xl font-bold">Recommended jobs <span class="bg-white border text-sm px-3 py-1 rounded-full ml-2">386</span></h1>
            <div class="text-sm text-gray-500 font-medium cursor-pointer">
              Sort by: <span class="text-black font-bold">Last updated <i class="fa-solid fa-sliders ml-1"></i></span>
            </div>
          </div>

          <div class="grid grid-cols-1 md:grid-cols-2 xl:grid-cols-3 gap-6">
            <JobCard v-for="(job, index) in jobs" :key="index" v-bind="job" />
          </div>
        </main>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const openDropdown = ref(null)
const selections = ref({
  location: 'All Countries',
  jobType: '',
  salary: ''
})


const scheduleOptions = [
  'Full time', 'Part time', 'Internship', 'Project work', 'Volunteering'
]

// NEW: Employment Type options
const employmentType = [
  'Full day', 'Flexible schedule', 'Shift work', 'Distant work', 'Shift method'
]

// NEW: Seniority Level options
const senioritylevel = [
  'Student', 'Junior', 'Middle', 'Senior', 'Lead'
]

const dropdownConfigs = [
  {
    key: 'location',
    label: 'All Countries',
    icon: '<path d="M17.657 16.657L13.414 20.9a1.998 1.998 0 01-2.827 0l-4.244-4.243a8 8 0 1111.314 0z" /><path d="M15 11a3 3 0 11-6 0 3 3 0 016 0z" />',
    options: ['United States', 'United Kingdom', 'Canada', 'Germany', 'France', 'Australia', 'Japan', 'Singapore', 'Cambodia', 'Remote']
  },
  {
    key: 'jobType',
    label: 'Job Type',
    icon: '<path d="M21 13.255A23.931 23.931 0 0112 15c-3.183 0-6.22-.62-9-1.745M16 6V4a2 2 0 00-2-2h-4a2 2 0 00-2 2v2m4 6h.01M5 20h14a2 2 0 002-2V8a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z" />',
    options: ['Full-time', 'Part-time', 'Contract', 'Freelance', 'Internship', 'Temporary', 'Volunteer', 'Commission', 'Hybrid', 'Seasonal']
  },
  {
    key: 'salary',
    label: 'Salary Range',
    icon: '<path d="M3 10h18M7 15h1m4 0h1m-7 4h12a2 2 0 002-2V5a2 2 0 00-2-2H6a2 2 0 00-2 2v12a2 2 0 002 2z" />',
    options: ['$0 - $1k', '$1k - $5k', '$5k - $10k', '$10k - $20k', '$20k - $40k', '$40k - $60k', '$60k - $80k', '$80k - $100k', '$100k - $150k', '$200k+']
  }
]

const jobs = ref([
  {
    date: '20 May, 2023',
    company: 'Amazon',
    companyIcon: 'fa-brands fa-amazon text-orange-500',
    title: 'Senior UI/UX Designer',
    tags: ['Part time', 'Senior level', 'Distant', 'Project work'],
    price: 250,
    location: 'San Francisco, CA',
    bgColor: 'bg-[#FFE2C5]'
  },
  {
    date: '4 Feb, 2023',
    company: 'Google',
    companyIcon: 'fa-brands fa-google text-blue-500',
    title: 'Junior UI/UX Designer',
    tags: ['Full time', 'Junior level', 'Distant', 'Project work'],
    price: 150,
    location: 'California, CA',
    bgColor: 'bg-[#D1F7EA]'
  },
  {
    date: '29 Jan, 2023',
    company: 'Dribbble',
    companyIcon: 'fa-brands fa-dribbble text-pink-500',
    title: 'Senior Motion Designer',
    tags: ['Part time', 'Senior level', 'Full Day', 'Shift work'],
    price: 260,
    location: 'New York, NY',
    bgColor: 'bg-[#E7DBFF]'
  },
  {
    date: '20 May, 2023',
    company: 'Amazon',
    companyIcon: 'fa-brands fa-amazon text-orange-500',
    title: 'Senior UI/UX Designer',
    tags: ['Part time', 'Senior level', 'Distant', 'Project work'],
    price: 250,
    location: 'San Francisco, CA',
    bgColor: 'bg-[#FFE2C5]'
  },
  {
    date: '4 Feb, 2023',
    company: 'Google',
    companyIcon: 'fa-brands fa-google text-blue-500',
    title: 'Junior UI/UX Designer',
    tags: ['Full time', 'Junior level', 'Distant', 'Project work'],
    price: 150,
    location: 'California, CA',
    bgColor: 'bg-[#D1F7EA]'
  },
  {
    date: '29 Jan, 2023',
    company: 'Dribbble',
    companyIcon: 'fa-brands fa-dribbble text-pink-500',
    title: 'Senior Motion Designer',
    tags: ['Part time', 'Senior level', 'Full Day', 'Shift work'],
    price: 260,
    location: 'New York, NY',
    bgColor: 'bg-[#E7DBFF]'
  },
])
</script>