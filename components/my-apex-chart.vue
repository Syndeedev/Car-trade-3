
<template>
  <apexchart
    type="area"
    :options="chartOptions"
    :series="series"
    height="500"
  />
</template>
<script setup >
const series = [
  {
    name: "series1",
    // data: [15, 72, 45, 32, 34, 52, 41],
    data: [
      [1334181600000, 33.55],
      [1334268000000, 33.18],
      [-1334527200000, 32.84],
      [1334613600000, 33.84],
      [1334700000000, 33.39],
      [1334786400000, 32.91],
      [1334872800000, 33.06],
      [1335132000000, 32.62],
      [1335218400000, 32.4],
      [-1335304800000, 33.13],
      [1335391200000, 33.26],
      [1335477600000, 33.58],
      [1335736800000, 33.55],
      [1335823200000, 33.77],
      [1335909600000, 33.76],
      [1335996000000, 33.32],
      [1336082400000, 32.61],
      [1336341600000, 32.52],
      [1336428000000, 32.67],
      [1336514400000, 32.52],
      [1336600800000, 31.92],
      [1336687200000, 32.2],
      [1336946400000, 32.23],
      [1337032800000, 32.33],
      [1337119200000, 32.36],
      [1337205600000, 32.01],
      [1337292000000, 31.31],
      [1337551200000, 32.01],
      [1337637600000, 32.01],
      [1337724000000, 32.18],
      [1337810400000, 31.54],
      [1337896800000, 31.6],
      [1338242400000, 32.05],
      [1338328800000, 31.29],
      [1338415200000, 31.05],
      [1338501600000, 29.82],
      [1338760800000, 30.31],
      [1338847200000, 30.7],
      [1338933600000, 31.69],
    ],
  },
];

const chartOptions = {
  chart: {
    id: "area-datetime",
    type: "area",
    height: 500,
    zoom: {
      enabled: false,
      //   autoScaleYaxis: true,
    },
    toolbar: {
      show: false,
    },
  },
  stroke: {
    show: true,
    curve: "smooth",
    width: 2,
  },
  annotations: {
    // yaxis: [
    //   {
    //     y: 30,
    //     borderColor: "#999",
    //     label: {
    //       show: true,
    //       text: "Support",
    //       style: {
    //         color: "#fff",
    //         background: "#00E396",
    //       },
    //     },
    //   },
    // ],
    // xaxis: [
    //   {
    //     x: new Date("14 Nov 2012").getTime(),
    //     borderColor: "#999",
    //     yAxisIndex: 0,
    //     label: {
    //       show: true,
    //       text: "Rally",
    //       style: {
    //         color: "#fff",
    //         background: "#775DD0",
    //       },
    //     },
    //   },
    // ],
  },
  colors: ["#0EA472"],
  dataLabels: {
    enabled: false,
  },
  markers: {
    size: 0,
    style: "hollow",
  },
  xaxis: {
    type: "datetime",
    min: new Date("01 Mar 2012").getTime(),
    tickAmount: 6,
  },
  yaxis: {
    labels: {
      formatter: function (value) {
        return `${value} units`;
      },
    },
  },
  tooltip: {
    x: {
      format: "dd MMM yyyy",
    },
  },
  fill: {
    type: "gradient",
    gradient: {
      shadeIntensity: 1,
      opacityFrom: 0.7,
      opacityTo: 0.1,
      stops: [10, 70, 100],
    },
  },
  plotOptions: {
    area: {
      fillTo: "end",
    },
  },
};
</script>


