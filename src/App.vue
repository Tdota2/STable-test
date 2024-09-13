<template>
  <s-table v-model:pagination="pagination" :columns="columns" :data-source="data" :height="400" @change="change">
    <template #bodyCell="{ column, text, record }">
      <template v-if="column.key === 'action'">
        <a-space size="middle">
          <a>Invite {{ record.name }}</a>
          <a>Delete</a>
        </a-space>
      </template>
      <template v-else-if="column.key === 'name'">
        <a>{{ text }}</a>
      </template>
      <template v-else-if="column.key === 'tags'">
        <span>
          <a-tag
            v-for="tag in text"
            :key="tag"
            :color="tag === 'loser' ? 'volcano' : tag.length > 5 ? 'geekblue' : 'green'"
          >
            {{ tag.toUpperCase() }}
          </a-tag>
        </span>
      </template>
    </template>
  </s-table>
</template>
<script lang="ts">
import type { STablePaginationConfig } from '@surely-vue/table';
import { defineComponent, onMounted, ref } from 'vue';

interface DataItem {
  key: string;
  name: string;
  age: number;
  address: string;
  tags: string[];
}

export default defineComponent({
  setup() {
    const columns = [
      {
        title: 'Name',
        dataIndex: 'name',
        key: 'name',
      },
      {
        title: 'Age',
        dataIndex: 'age',
        key: 'age',
      },
      {
        title: 'Address',
        dataIndex: 'address',
        key: 'address',
      },
      {
        title: 'Tags',
        key: 'tags',
        dataIndex: 'tags',
      },
      {
        title: 'Action',
        key: 'action',
      },
    ];
    const data = ref<DataItem[]>([]);

    const pagination = ref<STablePaginationConfig>({
      showQuickJumper: true,
      showSizeChanger: true,
      showTotal: (total) => `Total ${total} items`,
      pageSize: 20,
    });

    const change = () => {
      console.log(1111111);
    };

    const init = () => {
      data.value = [
        {
          key: '1',
          name: 'John Brown',
          age: 32,
          address: 'New York No. 1 Lake Park',
          tags: ['nice', 'developer'],
        },
        {
          key: '2',
          name: 'Jim Green',
          age: 42,
          address: 'London No. 1 Lake Park',
          tags: ['loser'],
        },
        {
          key: '3',
          name: 'Joe Black',
          age: 32,
          address: 'Sidney No. 1 Lake Park',
          tags: ['cool', 'teacher'],
        },
      ];
      for (let i = 0; i < 1000; i++) {
        const num = data.value.length + 1;
        data.value.push({
          key: String(num),
          name: `John Brown ${num}`,
          age: i + 1,
          address: `London Park no. ${num}`,
          tags: ['cool', 'teacher', 'loser'],
        });
      }
      console.log('init111111');
    };

    onMounted(() => {
      init();
    });
    return {
      data,
      columns: ref(columns),
      pagination,
      change,
    };
  },
});
</script>
