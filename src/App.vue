<template>
  <s-table
    :columns="columns"
    :scroll="{ y: 400 }"
    :pagination="false"
    :data-source="dataSource"
    :row-selection="rowSelection"
    default-expand-all-rows
  ></s-table>
</template>
<script lang="ts" setup>
import { STableProps } from "@surely-vue/table";
import { ref } from "vue";
const columns = [
  {
    title: "Full Name",
    dataIndex: "name",
  },
  {
    title: "Age",
    dataIndex: "age",
  },
];
const dataSource = ref([
  {
    key: 0,
    name: "001",
    age: 1,
    children: [
      {
        key: 1,
        name: "001-1",
        age: 2,
      },
    ],
  },
  { key: 2, name: "002", age: 3 },
]);

const rowSelection: STableProps["rowSelection"] = {
  checkStrictly: false,
  getCheckboxProps: (record: any) => ({
    disabled: record.key === 1, // Column configuration not to be checked
  }),
};
</script>
