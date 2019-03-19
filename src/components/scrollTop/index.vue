<template>
  <ScrollTop
    :pageIndex="pageIndex"
    :pageSize="pageSize"
    :loading="loading"
    :list="list"
    @getList="getList"
   />
</template>

<script>
import axios from 'axios';
import ScrollTop from './scrollTop'
export default {
  data() {
    return {
      pageIndex: 1,
      pageSize: 10,
      loading: true,
      list: [],
    }
  },
  components: {
    ScrollTop
  },
  methods: {
    getList() {
      this.loading = false
      axios.get(this.Host+'/jp-HCZZ-SituationDashboard-app-ms/park/getPersonsByStation', {
        params: {
          stationId: '71a36bca-d0da-4299-a881-275c738737df',
          starttime: '2019-03-19T00:00:00.0000000+08:00',
          personTypes: '',
          endtime: '2019-03-19T15:36:47.0000000+08:00',
          pageIndex: this.pageIndex,
          pageSize: this.pageSize
        }
      }).then((res) => {
        this.pageIndex++;
        this.loading = true
        res.data.data.data.map((val) => {
          this.list.push('https://ss2.baidu.com/6ONYsjip0QIZ8tyhnq/it/u=1830591836,2255339542&fm=85&app=63&f=JPEG?w=121&h=75&s=B807B156D525331B20AF93860200A0CB')
        })
      })
    },
  }
}
</script>
