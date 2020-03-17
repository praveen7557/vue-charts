
<script>
import { Line } from "vue-chartjs";
import { ptps } from "../samples/ptp";

Array.prototype.groupBy = function(key) {
  return this.reduce(function(rv, x) {
    (rv[x[key]] = rv[x[key]] || []).push(x);
    return rv;
  }, {});
};

Array.prototype.uniq = function() {
  return [...new Set(this)];
};

export default {
  extends: Line,
  props: ["options"],
  data() {
    return {
      gradient: null
    };
  },
  mounted() {
    let chartData = this.formatData(ptps);

    this.renderChart(chartData, {
      ...this.options,
      lineTension: 0,
      borderJoinStyle: "bevel",
      bezierCurve: false,
      scales: {
        yAxes: [
          {
            display: true,
            position: "right",
            ticks: {
              beginAtZero: false
            }
          }
        ],
        xAxes: [
          {
            display: true,
            gridLines: {
              display: false
            }
          }
        ]
      },
      tooltips: {
        callbacks: {
          title: function(tooltipItem, data) {
            return "";
          },
          label: function(tooltipItem, data) {
            return data.datasets[tooltipItem.datasetIndex].data[
              tooltipItem.index
            ];
          }
        },
        titleFontSize: 16,
        bodyFontSize: 14,
        displayColors: false
      },
      legend: {
        position: "bottom",
        labels: {
          boxWidth: 3,
          usePointStyle: true
        }
      },
      setPointStyle: true
    });
  },
  methods: {
    formatData(ptps) {
      let colors = {
        approved: "#46e0b5",
        rejected: "#e82b59",
        unreviewed: "#f9b127",
        revised_approved: "#3b96d2"
      };
      ptps = ptps.filter(e => e.category !== "Total");
      const labels = ptps.map(e => e.period_label).uniq();
      ptps = ptps.groupBy("category");

      const datasets = [];

      for (const key in ptps) {
        let keyName = key.toLowerCase().replace("/", "_");
        let obj = {
          lineTension: 0.2,
          pointRadius: 2,
          pointHoverRadius: 2,
          pointBackgroundColor: colors[keyName],
          fill: false,
          borderWidth: 2,
          label: key,
          borderColor: colors[keyName]
        };
        obj.data = ptps[key].map(e => e.count);
        if (keyName === "approved") {
          obj.backgroundColor = "rgba(242, 250, 242, 0.6)";
          obj.fill = true;
        }
        datasets.push(obj);
      }
      return {
        labels,
        datasets
      };
    }
  }
};
</script>
