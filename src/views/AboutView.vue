<template>
  <a-table :columns="columns" :data-source="accounts">
    <template #headerCell="{ column }">
      <template v-if="column.key === 'name'">
        <span>
          <smile-outlined />
          Name
        </span>
      </template>
    </template>

    <template #bodyCell="{ column, record }">
      <template v-if="column.key === 'name'">
        <a>
          {{ record.name }}
        </a>
      </template>
      <template v-else-if="column.key === 'tags'">
        <span>
          <a-tag
              v-for="tag in record.tags"
              :key="tag"
              :color="tag === 'loser' ? 'volcano' : tag.length > 5 ? 'geekblue' : 'green'"
          >
            {{ tag.toUpperCase() }}
          </a-tag>
        </span>
      </template>
      <template v-else-if="column.key === 'action'">
        <span>
          <a>Invite 一 {{ record.name }}</a>
          <a-divider type="vertical" />
          <a>Delete</a>
          <a-divider type="vertical" />
          <a class="ant-dropdown-link">
            More actions
            <down-outlined />
          </a>
        </span>
      </template>
    </template>
  </a-table>
</template>

<script lang="ts">
import { SmileOutlined, DownOutlined } from '@ant-design/icons-vue';
import { defineComponent,onMounted,ref} from 'vue';
import axios from 'axios';
const baseUrl = 'http://localhost:8085/account';

const columns = [
  {
    name: 'Name',
    dataIndex: 'name',
    key: 'name',
  },
  {
    title: 'Username',
    dataIndex: 'username',
    key: 'username',
  },
  {
    title: 'Gender',
    dataIndex: 'gender',
    key: 'gender',
  },
  {
    title: 'Email',
    key: 'email',
    dataIndex: 'email',
  },
  {
    title: 'Action',
    key: 'action',
  },
];


export default defineComponent({
  data() {
    return {
      accounts: [],

      valueAdd: {

        username: '',
        name: '',
        password: '',
        gender: '',
        email: '',
        phone: '',
        status: '',
      },
      valueEdit: {
        id: '',
        username: '',
        name: '',
        password: '',
        gender: '',
        email: '',
        phone: '',
      },
      errors:{
        username: '',
        name: '',
        password: '',
        gender: '',
        email: '',
        phone: '',
      },
      columns,
    }
  },

  async created() {
    this.getAll()
  },

  components: {
    SmileOutlined,
    DownOutlined,
  },


  methods: {
    async getAll() {
       await axios.get(`${baseUrl}/all`)
          .then(response => {
            console.log(response)
            this.accounts = response.data.data;
            console.log(this.accounts)
          })
          .catch(error => {
            console.log(error);
          })
    },
  },
  // setup() {
  //   return {
  //     data=,
  //     columns,
  //   };
  // },
  mounted() {
    this.getAll();
  }
});
</script>
