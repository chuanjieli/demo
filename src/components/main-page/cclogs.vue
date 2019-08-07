<template>
  <div style="padding: 10px;background: #f8f8f9">
    <Card title="CC日志" :padding="0" shadow>
      <Form ref="form" :model="form" inline label-position="right" style="margin-top:20px">
        <FormItem label="应用" :label-width="50">
          <Select v-model="form.list[0]" style="width:180px">
            <Option v-for="item in form.list" :value="item" :key="item">{{item}}</Option>
          </Select>
        </FormItem>
        <FormItem label="开始时间(00:00:00)" :label-width="115">
          <Date-picker
            type="date"
            format="yyyy/MM/dd"
            :value="new Date()"
            :options="options"
            :editable="false"
            @on-change="handleChange"
          ></Date-picker>
        </FormItem>
        <FormItem label="结束时间(23:59:59)" :label-width="115">
          <Date-picker
            type="date"
            format="yyyy/MM/dd"
            :value="new Date()"
            :options="options"
            :editable="false"
            @on-change="handleChange1"
          ></Date-picker>
        </FormItem>
        <FormItem :label-width="10">
          <Button type="primary">查询CC日志</Button>
        </FormItem>
      </Form>
      <Table
        stripe
        @on-row-click="showdetail"
        :columns="column"
        :data="data1"
        style="margin:0 10px;cursor:pointer"
      ></Table>
      <div style="margin: 10px;overflow: hidden">
        <div style="float: right;margin-bottom:20px">
          <Page :total="total" :current="1" @on-change="changePage"></Page>
        </div>
      </div>
    </Card>
  </div>
</template>
<script>
export default {
  name: 'cclogs',
  data() {
    return {
      options: {
        disabledDate(date) {
          return date && date.valueOf() > Date.now()
        }
      },
      form: {
        list: ['guamgmu', 'hedun', 'pogou']
      },
      column: [
        {
          title: 'ID编号',
          key: 'id'
          // render: (h, params) => {
          //   return h('span', [
          //     h(
          //       'router-link',
          //       {
          //         props: {
          //           // type: "primary",
          //           // size: "small",
          //           tag: 'a',
          //           to: '/logsdetail/cc/' + params.row.id
          //         },
          //         style: {
          //           marginRight: '5px'
          //         },
          //         on: {
          //           click: () => {
          //             // this.show(params.index);
          //           }
          //         }
          //       },
          //       params.row.id
          //     )
          //   ])
          // }
        },
        {
          title: '时间',
          key: 'time'
        },
        {
          title: '客户端IP',
          key: 'ip'
        },
        {
          title: '请求方式',
          key: 'type'
        },
        {
          title: '主机',
          key: 'host'
        },
        {
          title: 'URL路径',
          key: 'url'
        },
        {
          title: '防御动作',
          key: 'defense'
        }
      ],
      data: [
        {
          id: '1',
          time: '2019-07-19',
          ip: '10.1.4.51',
          type: 'get',
          host: 'host',
          url: 'src/index.html',
          defense: 'defense'
        },
        {
          id: '2',
          time: '2019-07-19',
          ip: '10.1.4.52',
          type: 'post',
          host: 'host',
          url: 'application/index.php',
          defense: 'defense'
        },
        {
          id: '3',
          time: '2019-07-19',
          ip: '10.1.4.59',
          type: 'get',
          host: 'host',
          url: 'home/report.html',
          defense: 'defense'
        },
        {
          id: '4',
          time: '2019-07-19',
          ip: '10.1.4.84',
          type: 'get',
          host: 'host',
          url: 'app/index.php',
          defense: 'defense'
        },
        {
          id: '5',
          time: '2019-07-19',
          ip: '10.1.4.95',
          type: 'post',
          host: 'host',
          url: 'user.html',
          defense: 'defense'
        },
        {
          id: '6',
          time: '2019-07-19',
          ip: '10.1.4.99',
          type: 'get',
          host: 'host',
          url: 'waflogs.html',
          defense: 'defense'
        },
        {
          id: '7',
          time: '2019-07-19',
          ip: '10.1.4.57',
          type: 'post',
          host: 'host',
          url: 'waf.html',
          defense: 'defense'
        },
        {
          id: '8',
          time: '2019-07-19',
          ip: '10.1.4.51',
          type: 'get',
          host: 'host',
          url: 'src/index.html',
          defense: 'defense'
        },
        {
          id: '9',
          time: '2019-07-19',
          ip: '10.1.4.52',
          type: 'post',
          host: 'host',
          url: 'application/index.php',
          defense: 'defense'
        },
        {
          id: '10',
          time: '2019-07-19',
          ip: '10.1.4.59',
          type: 'get',
          host: 'host',
          url: 'home/report.html',
          defense: 'defense'
        },
        {
          id: '11',
          time: '2019-07-19',
          ip: '10.1.4.84',
          type: 'get',
          host: 'host',
          url: 'app/index.php',
          defense: 'defense'
        },
        {
          id: '12',
          time: '2019-07-19',
          ip: '10.1.4.95',
          type: 'post',
          host: 'host',
          url: 'user.html',
          defense: 'defense'
        },
        {
          id: '13',
          time: '2019-07-19',
          ip: '10.1.4.99',
          type: 'get',
          host: 'host',
          url: 'waflogs.html',
          defense: 'defense'
        },
        {
          id: '14',
          time: '2019-07-19',
          ip: '10.1.4.57',
          type: 'post',
          host: 'host',
          url: 'waf.html',
          defense: 'defense'
        }
      ],
      data1: [],
      total: 10
    }
  },
  created() {
    this.total = this.data.length
    this.data1 = this.data.slice(0, 10)
  },
  methods: {
    handleChange(date) {
      console.log(date)
    },
    handleChange1(date) {
      console.log(date)
    },
    showdetail(params) {
      let url = 'logsdetail/cc/' + params.id
      this.$router.push(url)
    },
    changePage(num) {
      let page = (num - 1) * 10
      this.data1 = this.data.slice(page, page + 10)
    }
  }
}
</script>

