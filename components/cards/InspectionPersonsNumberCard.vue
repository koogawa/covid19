<template>
  <v-col cols="12" md="6" class="DataCard">
    <time-bar-chart
      :title="$t('検査実施人数')"
      :title-id="'number-of-inspection-persons'"
      :chart-id="'number-of-inspection-persons'"
      :chart-data="graphData"
      :date="data.date"
      :unit="$t('人')"
    >
      <template v-slot:description>
        <ul>
          <li>
            <t-i18n>
              {{ $t('（注）医療機関が保険適用で行った検査は含まれていない') }}
            </t-i18n>
          </li>
          <li>
            <t-i18n>
              {{
                $t(
                  '（注）現時点では日別のデータが公開されていないため、総数のみ表示しています。検査実施数は、速報値として公開するものであり、後日確定データとして修正される場合があります'
                )
              }}
            </t-i18n>
          </li>
          <li>
            <t-i18n>
              {{
                $t(
                  '（注）速報値として公開するものであり、後日確定データとして修正される場合あり'
                )
              }}
            </t-i18n>
          </li>
        </ul>
      </template>
    </time-bar-chart>
  </v-col>
</template>

<script>
import Data from '@/data/data.json'
import formatGraph from '@/utils/formatGraph'
import TimeBarChart from '@/components/TimeBarChart.vue'
import TI18n from '@/components/TI18n.vue'

export default {
  components: {
    TimeBarChart,
    TI18n
  },
  data() {
    const formatData = Data.inspection_persons.labels.map((date, i) => {
      return {
        日付: date,
        小計: Data.inspection_persons.datasets[0].data[i]
      }
    })

    // 検査実施人数グラフ
    const graphData = formatGraph(formatData)

    return {
      data: Data.inspection_persons,
      graphData
    }
  }
}
</script>
