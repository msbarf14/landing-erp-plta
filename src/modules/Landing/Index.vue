<template>
    <div class="relative overflow-hidden min-h-screen bg-white dark:bg-gray-800 pb-32">
      <div class="max-w-6xl relative z-20 mx-auto px-6 pt-24 pb-10 flex justify-between items-center">
        <div class="items-center flex space-x-4">
          <LtaLogo class="w-10 h-10 lg:w-16 lg:h-16 mx-auto text-gray-700 dark:text-white" isEdit/>
          <div class="text-left text-gray-700 dark:text-white">
            <p class="text-sm lg:text-3xl font-bold font-sans ">ERP SYSTEMS</p>
            <p class="text-sm lg:text-xl font-semibold font-sans">LAUT TIMUR ARDIPRIMA</p>
          </div>
        </div>
        <div class="flex space-x-2 items-center">
          <button type="button" @click="toggleDark">
            <SunIcon v-if="!isDark" class="w-10"/>
            <MoonIcon v-else class="w-10 text-sky-500"/>
          </button>
        </div>
      </div>
      <div class="max-w-6xl relative z-20 mx-auto px-6 py-20">
        <div class="grid gap-4 grid-cols-1 md:grid-cols-4">
          <!-- ERP LTA -->
          <a 
            v-for="item in data"
            :href="item.link"
            target="_blank"
            class="py-3 px-4 w-full bg-white dark:bg-gray-900 border border-gray-300 dark:border-gray-800 rounded-lg shadow-xl shadw-gray-200 dark:shadow-gray-800 group hover:bg-gray-800 dark:hover:bg-sky-800">
            <div class="flex items-center space-x-2">
              <div class="aspect-square overflow-hidden">
                <component :is="item.icon()"></component>
              </div>
              <div >
                <p class="uppercase text-sm text-gray-400 dark:text-gray-200 group-hover:text-gray-100">{{item.category}}</p>
                <p class="uppercase text-lg font-semibold text-gray-800 dark:text-sky-500 group-hover:text-white">{{item.title}}</p>
              </div>
            </div>
          </a>
        </div>
      </div>
      <div class="fixed w-full -top-[8rem] opacity-70">
        <Pattern class=" w-[250%]  md:w-[200%] lg:w-[100%] lg:mt-[15rem]"/>
      </div>
    </div>
  </template>
  
  <script setup>
  import {ref} from "vue"
  import { SunIcon, MoonIcon } from '@heroicons/vue/24/outline'
  import { useDark } from '@vueuse/core'
  
  import LtaLogo from "../../components/LtaLogo.vue"
  import Pattern from "../../components/Pattern.vue"
  import IconSap from "../../components/IconSap.vue"
  import IconSfa from "../../components/IconSfa.vue"
  import IconMmr from "../../components/IconMmr.vue"
  import IconPaltafile from "../../components/IconPaltafile.vue"
  import IconFacture from "../../components/IconFacture.vue"
  import IconSpvDashboard from "../../components/IconSpvDashboard.vue"
  import IconCollector from "../../components/IconCollector.vue"
  
  const data = ref([
    { title: 'ERP LTA', category: 'Inventory', link: '#', status: 'running', icon: () => IconSap},
    { title: 'ERP TAA', category: 'Inventory', link: '#', status: 'running', icon: () =>  IconSap},
    { title: 'SFA PORTAL', category: 'Web Apps', link: '#', status: 'running', icon: () =>  IconSfa},
    { title: 'MMR PWA', category: 'Mobile Apps', link: 'http://mmr.avenzhore.space', status: 'running', icon: () =>  IconMmr},
    { title: 'E-FACTURE', category: 'Web Apps', link: 'https://faktur.erplta.com/public/login', status: 'running', icon: () =>  IconFacture},
    { title: 'COLLECTOR', category: 'Mobile Apps', link: '', status: 'running', icon: () =>  IconCollector},
    { title: 'E-CONTRACT', category: 'Web Apps', link: '', status: 'running', icon: () =>  IconPaltafile},
    { title: 'SPV PORTAL', category: 'Mobile Apps', link: '', status: 'running', icon: () =>  IconSpvDashboard},
  ])
  
  const isDark = useDark()
  const toggleDark = () => {
    isDark.value = !isDark.value
  }
  
  </script>