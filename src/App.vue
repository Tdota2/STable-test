<template>
  <s-table
    :columns="columns"
    :data-source="dataSource"
    :rowHeight="() => {
            return 80
      }"
  ></s-table>
</template>
<script lang="ts">
import { defineComponent, ref } from 'vue';

interface DataItem {
  key: string;
  name: string;
  money: string;
  address: string;
  children?: Array<DataItem>;
}

export default defineComponent({
  setup() {
    const columns = [
      {
        title: 'Name',
        dataIndex: 'name',
        autoHeight: true,
      },
      {
        title: 'Cash Assets',
        dataIndex: 'money',
        align: 'right',
      },
      {
        title: 'Address',
        dataIndex: 'address',
      },
    ];
    const data: DataItem[] = [
      {
        key: '1',
        name: 'John Brown',
        money: '￥300,000.00',
        address: 'New York No. 1 Lake Park',
        children: [
          {
            key: '11',
            name: 'John Brown1',
            money: '￥3400,000.00',
            address: 'New York No. 11 Lake Park',
          },
        ],
      },
      {
        key: '2',
        name: 'Jim Green',
        money: '￥1,256,000.00',
        address: 'London No. 1 Lake Park',
      },
      {
        key: '3',
        name: 'Joe Black',
        money: '￥120,000.00',
        address: 'Sidney No. 1 Lake Park',
      },
      {
        key: '4',
        name: 'Tom',
        money: '￥186,000.00',
        address: 'Sidney No. 2 Lake Park',
      },
      {
        key: '5',
        name: 'Tony',
        money: '￥110,000.00',
        address: 'Sidney No. 2 Lake Park',
      },
      {
        key: '6',
        name: 'YaYa',
        money: '￥200,000.00',
        address: 'Sidney No. 4 Lake Park',
      },
    ];
    return {
      dataSource: data,
      columns: ref(columns),
    };
  },
});
</script>
