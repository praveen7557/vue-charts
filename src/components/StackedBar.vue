
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
    this.renderChart(
      {
        labels: ["Red", "Blue", "Yellow", "Green", "Purple", "Orange"],
        // labels: ["Red"],
        datasets: [
          {
            label: "# of Votes 1",
            data: [
              [713, 978],
              [819, 988],
              [902, 1023],
              [858, 1200],
              [799, 900],
              [700, 900]
            ],
            backgroundColor: [
              "#e82a59",
              "#e82a59",
              "#e82a59",
              "#e82a59",
              "#e82a59",
              "#e82a59"
            ],
            borderWidth: 0
          },
          {
            label: "# of Votes 2",
            data: [
              [978 - 978, 1300 - 978],
              [988 - 988, 1400 - 988],
              [1023 - 1023, 1500 - 1023],
              [1200 - 1200, 1600 - 1200],
              [900 - 900, 1100 - 900],
              [900 - 900, 1567 - 900]
            ],
            backgroundColor: [
              "#c4224a",
              "#c4224a",
              "#c4224a",
              "#c4224a",
              "#c4224a",
              "#c4224a"
            ],
            borderWidth: 0
          }
        ]
      },
      {
        ...this.options,
        cornerRadius: 4,
        scales: {
          xAxes: [
            {
              stacked: true, // this should be set to make the bars stacked
              gridLines: {
                // You can change the color, the dash effect, the main axe color, etc.
                borderDash: [8, 4],
                color: "#eeeeee"
              }
            }
          ],
          yAxes: [
            {
              stacked: true,
              gridLines: {
                color: "#eaeaea"
              },
              ticks: {
                min: 600,
                stepSize: 600,
                max: 1800
              }
            }
          ]
        }
      }
    );
  }
};
</script>
