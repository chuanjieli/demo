<template>
  <div style="padding: 10px;background: #f8f8f9">
    <Card title="WAF日志" :padding="0" shadow>
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
          <Button type="primary">查询WAF日志</Button>
        </FormItem>
      </Form>
      <Table
        stripe
        @on-row-click="showdetail"
        :columns="column"
        :data="data"
        style="margin:0 10px;"
      ></Table>
      <div style="margin: 10px;overflow: hidden">
        <div style="float: right;margin-bottom:20px">
          <Page :total="100" :current="1" @on-change="changePage"></Page>
        </div>
      </div>
    </Card>
  </div>
</template>
<script>
export default {
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
        },
        {
          title: '时间',
          key: 'time'
        },
        {
          title: 'IP地址',
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
        },
        {
          title: '策略ID',
          key: 'tactics'
        }
      ],
      data: [
        {
          id: '1',
          time: '2019-07-18',
          ip: '10.1.4.51',
          type: 'post',
          host: 'host',
          url: 'index.html',
          defense: 'defense',
          tactics: '1'
        },
        {
          id: '2',
          time: '2019-07-18',
          ip: '10.1.4.52',
          type: 'get',
          host: 'host',
          url: 'index.php',
          defense: 'defense',
          tactics: '2'
        },
        {
          id: '3',
          time: '2019-07-18',
          ip: '10.1.4.53',
          type: 'get',
          host: 'host',
          url: 'home/index.html',
          defense: 'defense',
          tactics: '3'
        },
        {
          id: '4',
          time: '2019-07-18',
          ip: '10.1.4.54',
          type: 'post',
          host: 'host',
          url: 'hedun.py',
          defense: 'defense',
          tactics: '4'
        },
        {
          id: '5',
          time: '2019-07-18',
          ip: '10.1.4.55',
          type: 'get',
          host: 'host',
          url: 'app/detail.html',
          defense: 'defense',
          tactics: '5'
        },
        {
          id: '6',
          time: '2019-07-18',
          ip: '10.1.4.56',
          type: 'post',
          host: 'host',
          url: 'src/assets/sffdg.png',
          defense: 'defense',
          tactics: '6'
        },
        {
          id: '7',
          time: '2019-07-18',
          ip: '10.1.4.57',
          type: 'get',
          host: 'host',
          url: 'waf/screen.html',
          defense: 'defense',
          tactics: '7'
        }
      ]
    }
  },
  methods: {
    handleChange(date) {
      console.log(date)
    },
    handleChange1(date) {
      console.log(date)
    },
    showdetail(params) {
      let url = 'logsdetail/waf/' + params.id
      this.$router.push(url)
    },
    changePage() {}
  }
}
</script>