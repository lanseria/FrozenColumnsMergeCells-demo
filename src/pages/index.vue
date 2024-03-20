<script setup lang="ts">
import { uniqBy } from 'lodash-es'

const summaryTitleRenderData = [
  {
    label: '应出勤',
    unit: '小时',
    colspan: 1,
  },
  {
    label: '出勤',
    unit: '小时',
    colspan: 1,
  },
  {
    label: '迟到',
    unit: '次',
    colspan: 1,
  },
  {
    label: '早退',
    unit: '次',
    colspan: 1,
  },
  {
    label: '缺卡',
    unit: '次',
    colspan: 1,
  },
  {
    label: '旷工',
    unit: '次',
    colspan: 1,
  },
  {
    label: '公出',
    unit: '次',
    colspan: 2,
  },
  {
    label: '公出',
    unit: '小时',
    colspan: 2,
  },
  {
    label: '年休假',
    unit: '次',
    colspan: 2,
  },
  {
    label: '年休假',
    unit: '小时',
    colspan: 2,
  },
  {
    label: '请假',
    unit: '天',
    colspan: 1,
  },
  {
    label: '调休',
    unit: '天',
    colspan: 1,
  },
  {
    label: '加班',
    unit: '次',
    colspan: 1,
  },
  {
    label: '代班',
    unit: '次',
    colspan: 1,
  },
  {
    label: '换班：换出',
    unit: '次',
    colspan: 1,
  },
  {
    label: '换班：换入',
    unit: '次',
    colspan: 1,
  },
  {
    label: '浮动打卡',
    unit: '次',
    colspan: 1,
  },
]
interface IData {
  id: number
  deptName: string
  name: string
  dateData: { content: string }[]
  summaryData: string[]
}
const rowRenderData = [
  {
    date: '2024-01-01',
    week: '周一',
  },
  {
    date: '2024-01-02',
    week: '周二',
  },
  {
    date: '2024-01-03',
    week: '周三',
  },
  {
    date: '2024-01-04',
    week: '周四',
  },
  {
    date: '2024-01-05',
    week: '周五',
  },
  {
    date: '2024-01-06',
    week: '周六',
  },
]
const originalData: IData = {
  id: 1,
  deptName: '部门1',
  name: '张三',
  dateData: [
    {
      content: '出勤',
    },
    {
      content: '迟到',
    },
    {
      content: '早退',
    },
    {
      content: '缺卡',
    },
    {
      content: '缺卡',
    },
    {
      content: '缺卡',
    },
  ],
  summaryData: ['1', '2', '3', '4', '4', '4', '4', '4', '4', '4', '4', '4', '4', '4', '4', '4', '4'],
}

const renderData: IData[] = [
]
for (let i = 0; i < 100; i++) {
  const data: IData = {
    ...originalData,
    id: i + 1,
  }
  renderData.push(data)
}
// 进行过滤，如果summaryTitleRenderData中的colspan为2，则其label相同的会被合并
const uniqByLabel = uniqBy(summaryTitleRenderData, 'label')
</script>

<template>
  <div>
    <table class="fixed-width-table border-separate border-spacing-0 table-fixed">
      <thead>
        <tr>
          <th rowspan="3" class="sticky left-0 top-0 z-3 min-w-100px w-100px">
            部门
          </th>
          <th rowspan="3" class="sticky left-100px top-0 z-3 min-w-100px w-100px">
            姓名
          </th>
          <th :colspan="rowRenderData.length" class="sticky top-0 z-2 h-55px overflow-y-auto text-left!">
            <div class="max-h-50px min-h-50px px-20px py-10px text-16px">
              Hello World
            </div>
          </th>
          <th :colspan="summaryTitleRenderData.length" class="sticky top-0 z-2">
            <div class="px-20px py-10px text-20px">
              统计
            </div>
          </th>
        </tr>
        <tr>
          <th
            v-for="(item, index) in rowRenderData" :key="index" class="sticky top-55px z-2 min-w-100px"
          >
            {{ item.date }}
          </th>
          <th v-for="(item, index) in uniqByLabel" :key="index" :colspan="item.colspan" class="sticky top-55px z-2 min-w-100px text-size-12px">
            {{ item.label }}
          </th>
        </tr>
        <tr>
          <th
            v-for="(item, index) in rowRenderData" :key="index" class="sticky top-[calc(55px+26px)] z-2 min-w-100px"
          >
            {{ item.week }}
          </th>
          <th v-for="(item, index) in summaryTitleRenderData" :key="index" class="sticky top-[calc(55px+26px)] z-2 min-w-100px text-size-12px">
            ({{ item.unit }})
          </th>
        </tr>
      </thead>
      <tbody class="w-full overflow-auto">
        <tr v-for="item in renderData" :key="item.id">
          <td class="sticky left-0 top-0 z-2 min-w-100px w-100px">
            {{ item.deptName }}
          </td>
          <td class="sticky left-100px top-0 z-2 min-w-100px w-100px">
            {{ item.name }}
          </td>
          <td
            v-for="(td, index) in item.dateData" :key="index" class="relative text-size-12px"
          >
            <div class="whitespace-pre">
              {{ td.content }}
            </div>
          </td>
          <td v-for="(td, index) in item.summaryData" :key="index" class="text-size-12px">
            {{ td }}
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<style lang="css" scoped>
th {
  @apply bg-[var(--color-neutral-2)];
}
td {
  @apply bg-white;
}
th,
td {
  @apply py-2px;
}
th,
td {
  @apply border-l-none border-r-1px border-b-1px border-[var(--color-neutral-3)] text-center;
}
</style>
