
<script>
require("./RoundedBar");
import { Bar } from "vue-chartjs";

export default {
  extends: Bar,
  props: ["options"],
  data() {
    return {
      gradient: null
    };
  },
  mounted() {
    var refChart = this.$refs.canvas.getContext("2d");

    const getStart = (cur, max, total, height) => {
      return Math.abs(((max - cur) / total) * height);
    };

    // this.addPlugin({
    //   id: "my-plugin",
    //   beforeDatasetsUpdate: function(chart) {
    //     for (var i = 0; i < chart.config.data.datasets.length; i++) {
    //       // We store it
    //       var dataset = chart.config.data.datasets[i];
    //       // For every data in this dataset
    //       let colors = [...dataset.backgroundColor];
    //       for (var j = 0; j < dataset.data.length; j++) {
    //         // We store the data model (graph information)
    //         var meta = dataset._meta[0].data[j];
    //         var model = meta._model;
    //         var yScale = meta._yScale;
    //         // We use the model to get the left & right borders X position
    //         // and to create the gradient
    //         var startX = model.x,
    //           endX = model.x + model.width,
    //           startY = getStart(
    //             yScale.max,
    //             dataset.data[j],
    //             yScale._valueRange,
    //             yScale.height
    //           ),
    //           endY = getStart(yScale.max, 0, yScale._valueRange, yScale.height),
    //           gradient = refChart.createLinearGradient(
    //             startX,
    //             startY,
    //             endX - 5,
    //             endY - 5
    //           );
    //         console.log(startX, startY, endX, endY);
    //         // The colors of the gradient that were defined in the data
    //         gradient.addColorStop(0, colors[0]);
    //         gradient.addColorStop(1, colors[1]);
    //         // We set this new color to the data background
    //         dataset.backgroundColor[j] = gradient;
    //       }
    //     }
    //   }
    // });

    let gradient1 = this.$refs.canvas
      .getContext("2d")
      .createLinearGradient(0, 0, 0, 300);

    gradient1.addColorStop(0, "#7ae7c6");
    gradient1.addColorStop(0.5, "#c1e7bf");
    gradient1.addColorStop(1, "#fff");

    let gradient2 = this.$refs.canvas
      .getContext("2d")
      .createLinearGradient(0, 0, 0, 450);

    gradient2.addColorStop(0, "rgba(255, 177,33, 1)");
    gradient2.addColorStop(0.5, "rgba(255, 177, 33, 0.5)");
    gradient2.addColorStop(1, "rgba(255, 177, 33, 0)");

    this.renderChart(
      {
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
          "December"
        ],
        datasets: [
          {
            label: "Dataset 1",
            borderWidth: 1,
            backgroundColor: [...Array(12).keys()].map(i => gradient1),
            data: [60, 30, 40, 20, 80, 23, 33, 31, 45, 77, 12, 11]
          },
          {
            label: "Dataset 2",
            borderWidth: 1,
            backgroundColor: [...Array(12).keys()].map(i => gradient2),
            data: [22, 21, 33, 40, 10, 83, 13, 19, 54, 57, 62, 47]
          }
        ]
      },
      this.options
    );
  }
};
</script>
