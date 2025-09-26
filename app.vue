<template>
  <div>
    <NuxtRouteAnnouncer />
    <!--NAV BAR-->
    <header class="sticky top-0 z-50 space-x-1 border-b-0 bg-white shadow-md">
      <div class="flex justify-between items-center p-4">
        <a class="text-3xl font-mono" href="">Car trade</a>
        <button class="text-white bg-blue-500 px-8 py-2 rounded">Login</button>
      </div>
      <div class="py-2 px-4 bg-blue-500 flex justify-between items-center">
        <p class="text-yellow-400">Bua Foods</p>
        <p class="text-yellow-400">MTN</p>
        <p class="text-yellow-400">Zenith bank</p>
      </div>
    </header>

    <!-- <Line :data="chartData" :options="chartOptions" /> -->
  </div>
</template>
<script>
import { Bar, Line } from "vue-chartjs";
import {
  Chart as ChartJS,
  Title,
  Tooltip,
  Legend,
  BarElement,
  CategoryScale,
  LinearScale,
  PointElement,
  LineElement,
} from "chart.js";

ChartJS.register(
  Title,
  Tooltip,
  Legend,
  BarElement,
  CategoryScale,
  LinearScale,
  PointElement,
  LineElement
);

export default {
  components: { Bar, Line },
  data() {
    return {
      chartData: {
        labels: [
          "January",
          "February",
          "March",
          "April",
          "May",
          "June",
          "July",
          "August",
          "September",
          "October",
          "November",
          "December",
        ],
        datasets: [
          {
            type: "bar",
            label: "line Dataset",
            data: [75, 192, 192, 40, 662, 12, 75, 192, 192, 40, 20, 12],
            borderColor: "rgb(255, 99, 132)",
            backgroundColor: "rgba(255, 99, 132, 0.2)",
            order: 1,
          },
          {
            type: "bar",
            label: "Line Dataset",
            data: [95, 292, 392, 90, 162, 65, 175, 112, 192, 410, 120, 142],
            backgroundColor: "rgba(5, 99, 0, 0.4)",
            borderColor: "rgb(255, 99, 132)",
            order: 2,
          },
          {
            type: "bar",
            label: "Bar Dataset",
            data: [95, 292, 392, 90, 162, 65, 175, 112, 192, 410, 120, 142],
            backgroundColor: "rgba(125, 9, 132, 0.3)",
            borderColor: "rgb(255, 99, 132)",
            order: 3,
          },
        ],
        // datasets: [
        //   {
        //     data: [75, 192, 192, 40, 662, 12, 75, 192, 192, 40, 20, 12],
        //     borderColor: "rgb(75, 192, 192)",
        //     tension: 0.4,
        //   },
        // ],
      },
      chartOptions: {
        responsive: true,
      },
    };
  },
};
</script>
