<script setup>
import { reactive, ref } from "vue";
import axios from "axios"
import { LineChart } from 'vue-chart-3';
import { Chart, registerables} from "chart.js";


import Pattern from "../../components/Pattern.vue"
import LtaLogo from "../../components/LtaLogo.vue"

Chart.register(...registerables);
console.log(Chart.defaults)
const data = ref([])
const testData = reactive({
    labels: [],
    datasets: [
        {
            data: [],
            backgroundColor: '#ecfdf5',
            borderColor: '#059669',
            fill:true,
            label: 'Memory used /mb',
            tension: 0.3,
        },
    ],
})

const chartOptions = ref({
    plugins: {
      legend: {
         display: true,
      },
      title: {
        display: false
      }
   },
   scales: {
    y: {
        min: 0
    },
     x: {
           display: true,
         },
     },
})

const fetch = async () => {
    await axios.get('http://36.93.82.10/sapweb/api/monitor/memory')
    .then((res) => {
        res.data.map((item, index) => {
            testData.labels.push(Object.values(item)[1])
            testData.datasets[0].data.push(parseInt(Object.values(item)[0]))
            if(testData.labels.length > 51) {
                testData.labels.remove(index)
                testData.datasets[0].data.remove(index)
            }
        })
        
    }).catch((err) => {
        console.log()
    })
}

setInterval(() => {
    fetch()
}, 7000)





</script>
<template>
    <div class="relative overflow-hidden min-h-screen bg-white dark:bg-gray-800 pb-32">
        <div class="max-w-6xl relative z-20 mx-auto px-6 pt-24 pb-10">
            <div class="py-3 flex space-x-3 items-center py-6">
                <LtaLogo isEdit class="text-gray-800 w-16 h-16"/>
                <div>
                    <h1 class="text-2xl font-semibold text-gray-800">ERP SAP WEB LTA</h1>
                    <p>Performance monitor</p>
                </div>
            </div>
            <div class="w-full p-5 bg-white shadow-lg border rounded-lg">
                <LineChart :chartData="testData" :options="chartOptions"/>
            </div>
        </div>
        <div class="fixed w-full -top-[5rem]">
            <Pattern class=" w-[250%]  md:w-[200%] lg:w-[100%] lg:mt-[15rem]" />
        </div>
    </div>
</template>