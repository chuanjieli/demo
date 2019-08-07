<template>
  <div style="padding: 10px;background: #f8f8f9">
    <Card title="扫描日志" :padding="0" shadow>
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
          <Button type="primary">查询扫描日志</Button>
        </FormItem>
      </Form>
      <Table
        stripe
        @on-row-click="showdetail"
        :columns="column"
        :data="data1"
        style="margin:0 10px;"
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
  name: 'scanlogs',
  data() {
    return {
      options: {
        disabledDate(date) {
          return date && date.valueOf() > Date.now()
        }
      },
      total: 10,
      form: {
        list: ['guamgmu', 'hedun', 'pogou']
      },
      column: [
        {
          title: 'ID编号',
          key: 'id'
        },
        {
          title: '攻击时间',
          key: 'time'
        },
        {
          title: '攻击源IP地址',
          key: 'ip'
        },
        {
          title: '攻击方式',
          key: 'type'
        },
        {
          title: '被攻击网站',
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
          time: '2019-07-30',
          ip: '10.1.4.51',
          type: 'post',
          host: 'www.hedun.com',
          url: 'index.html',
          defense: 'Block'
        },
        {
          id: '2',
          time: '2019-07-30',
          ip: '10.1.4.52',
          type: 'get',
          host: 'www.hedun.com',
          url: 'index.php',
          defense: 'Block'
        },
        {
          id: '3',
          time: '2019-07-30',
          ip: '10.1.4.53',
          type: 'get',
          host: 'www.hedun.com',
          url: 'home/index.html',
          defense: 'Block'
        },
        {
          id: '4',
          time: '2019-07-30',
          ip: '10.1.4.54',
          type: 'post',
          host: 'www.hedun.com',
          url: 'hedun.py',
          defense: 'Block'
        },
        {
          id: '5',
          time: '2019-07-30',
          ip: '10.1.4.55',
          type: 'get',
          host: 'www.hedun.com',
          url: 'app/detail.html',
          defense: 'Block'
        },
        {
          id: '6',
          time: '2019-07-30',
          ip: '10.1.4.56',
          type: 'post',
          host: 'www.hedun.com',
          url: 'src/assets/sffdg.png',
          defense: 'Block'
        },
        {
          id: '7',
          time: '2019-07-30',
          ip: '10.1.4.57',
          type: 'get',
          host: 'www.hedun.com',
          url: 'waf/screen.html',
          defense: 'Block'
        },
        {
          id: '8',
          time: '2019-07-30',
          ip: '10.1.4.91',
          type: 'get',
          host: 'www.hedun.com',
          url: 'waf/screen.html',
          defense: 'Block'
        },
        {
          id: '9',
          time: '2019-07-30',
          ip: '10.1.4.91',
          type: 'get',
          host: 'www.hedun.com',
          url: 'waf/screen.html',
          defense: 'Block'
        },
        {
          id: '10',
          time: '2019-07-30',
          ip: '10.1.4.91',
          type: 'get',
          host: 'www.hedun.com',
          url: 'waf/screen.html',
          defense: 'Block'
        },
        {
          id: '11',
          time: '2019-07-30',
          ip: '10.1.4.91',
          type: 'get',
          host: 'www.hedun.com',
          url: 'waf/screen.html',
          defense: 'Block'
        },
        {
          id: '12',
          time: '2019-07-30',
          ip: '10.1.4.91',
          type: 'get',
          host: 'www.hedun.com',
          url: 'waf/screen.html',
          defense: 'Block'
        },
        {
          id: '13',
          time: '2019-07-30',
          ip: '10.1.4.91',
          type: 'get',
          host: 'www.hedun.com',
          url: 'waf/screen.html',
          defense: 'Block'
        },
        {
          id: '14',
          time: '2019-07-30',
          ip: '10.1.4.91',
          type: 'get',
          host: 'www.hedun.com',
          url: 'waf/screen.html',
          defense: 'Block'
        },
        {
          id: '15',
          time: '2019-07-30',
          ip: '10.1.4.91',
          type: 'get',
          host: 'www.hedun.com',
          url: 'waf/screen.html',
          defense: 'Block'
        },
        {
          id: '16',
          time: '2019-07-30',
          ip: '10.1.4.91',
          type: 'get',
          host: 'www.hedun.com',
          url: 'waf/screen.html',
          defense: 'Block'
        },
        {
          id: '17',
          time: '2019-07-30',
          ip: '10.1.4.91',
          type: 'get',
          host: 'www.hedun.com',
          url: 'waf/screen.html',
          defense: 'Block'
        },
        {
          id: '18',
          time: '2019-07-30',
          ip: '10.1.4.91',
          type: 'get',
          host: 'www.hedun.com',
          url: 'waf/screen.html',
          defense: 'Block'
        },
        {
          id: '19',
          time: '2019-07-30',
          ip: '10.1.4.91',
          type: 'get',
          host: 'www.hedun.com',
          url: 'waf/screen.html',
          defense: 'Block'
        },
        {
          id: '20',
          time: '2019-07-30',
          ip: '10.1.4.91',
          type: 'get',
          host: 'www.hedun.com',
          url: 'waf/screen.html',
          defense: 'Block'
        },
        {
          id: '21',
          time: '2019-07-30',
          ip: '10.1.4.87',
          type: 'get',
          host: 'www.waf.com',
          url: 'waf.html',
          defense: 'Block'
        }
      ],
      data1: []
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
      let url = 'logsdetail/scan/' + params.id
      this.$router.push(url)
    },
    changePage(num) {
      let page = (num - 1) * 10
      this.data1 = this.data.slice(page, page + 10)
    }
  }
}
</script>