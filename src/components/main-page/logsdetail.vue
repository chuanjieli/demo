<template>
  <div>
    <Row style="padding:10px" :gutter="16">
      <Col span="24">
        <Card :bordered="false">
          <p slot="title">日志详情</p>

          <Row style="padding:10px" :gutter="16">
            <Col span="12">
              <Card>
                <h4>基本信息</h4>
                <ul>
                  <li v-for="item,i in basic_data" :key="item">{{i + ' : ' + item }}</li>
                  <!-- <li>攻击源IP地址 : 106.13.46.67</li>
                  <li>攻击方式 : GET</li>
                  <li>被攻击网站 : www.hedun.top : 80</li>
                  <li>attack_url_path : /index.html</li>
                  <li>attack_url_query : id=1 and 1=1</li>
                  <li>attack_content_type : text/html; charset=utf-8</li>
                  <li>attack_user_agent : Mozilla/5.0 (Windows NT 6.1;)</li>
                  <li>Cookie : [xxx,xxx,xxx]</li>
                  <li>raw_request : xxxxxxxx</li>
                  <li>防御动作 : Block</li>
                  <li>扫描包大小 : 128</li>-->
                </ul>
              </Card>
            </Col>
            <Col span="12">
              <Card>
                <div v-if="scan_block">
                  <h4>扫描相关信息</h4>
                  <ul>
                    <li v-for="item,i in scan_info" :key="item">{{i + ' : ' + item }}</li>
                    <!-- <li>扫描工具 : nmap</li>
                    <li>扫描位置 : xxx</li>
                    <li>扫描工具描述 : xxxxxxxxx</li>
                    <li>扫描详情 : xxxxxx</li>-->
                  </ul>
                </div>
                <div v-if="attack_block">
                  <h4>攻击详情</h4>
                  <ul>
                    <li v-for="item,i in attack_info" :key="item">{{i + ' : ' + item }}</li>
                  </ul>
                </div>
                <div v-if="conf_block">
                  <h4>配置信息</h4>
                  <ul>
                    <li v-for="item,i in conf_info" :key="item">{{i + ' : ' + item }}</li>
                    <!-- <li>应用名称 : Hedun</li>
                    <li>协议类型 : http</li>
                    <li>防护域名 : www.hedun.top:80</li>
                    <li>检查点 : url_path</li>
                    <li>描述 : xxx</li>
                    <li>用户名 : hedun</li>-->
                  </ul>
                </div>
              </Card>
            </Col>
          </Row>

          <Button slot="extra" type="primary" @click="$router.go(-1)" size="small">&nbsp;返回&nbsp;</Button>
        </Card>
      </Col>
    </Row>
    <!-- <Spin size="large" fix v-if="spinShow"></Spin> -->
  </div>
</template>
<script>
export default {
  data() {
    return {
      msg: 'skdfjdk',
      data: {
        attack_time: '2019-05-05 02:34:54',
        attack_ip: '106.13.46.67',
        attack_method: 'GET',
        be_attack_host: 'www.hedun.top',
        attack_url_path: '/index.html',
        attack_url_query: 'id=1 and 1=1',
        attack_content_type: 'text/html; charset=utf-8;',
        attack_user_agent: 'Mozilla/5.0 (Windows NT 6.1;)',
        attack_cookies: '[xxx,xxx,xxx]',
        attack_raw_request: 'xxxxxxxx',
        action: 'Block',
        attack_flowsize: 128,
        attack_info: {
          vulntype: 'SQL Injection',
          description: 'SQL Injection with Search',
          attack_detail: 'xxx'
        },
        conf_info: {
          appname: 'Hedun',
          protocol: 'http',
          domain: 'www.hedun.top',
          check_point: 'url_path',
          description: 'hedun',
          username: 'xxx'
        },
        scan_info: {
          scan_tool: 'nmap',
          scan_positon: 'xxx',
          description: 'xxxxxxxxx',
          scan_detail: 'xxxxxx'
        }
      },
      basic_data: {},
      attack_info: {},
      attack_block: false,
      scan_info: {},
      scan_block: false,
      conf_info: {},
      conf_block: false
    }
  },
  created() {
    var bible = {
      attack_time: '攻击时间',
      attack_ip: '攻击源IP地址',
      attack_method: '攻击方式',
      be_attack_host: '被攻击网站',
      attack_url_path: '攻击URLPath',
      attack_url_query: '攻击URLQuery',
      attack_content_type: '攻击Content-type',
      attack_user_agent: 'UA',
      attack_cookies: 'Cookie',
      attack_raw_request: 'raw_request',
      action: '防御动作',
      attack_flowsize: '攻击包大小',
      access_time: '访问时间',
      access_ip: '客户端源IP地址',
      access_method: '访问方式',
      access_host: '访问网站',
      access_url_path: '访问URLPath',
      access_url_query: '访问URLQuery',
      access_content_type: '访问Content-type',
      access_user_agent: 'UA',
      access_cookies: 'Cookie',
      access_raw_request: 'raw_request',
      response_time: '响应时间',
      response_status: '响应状态',
      inflow_datasize: '请求包大小',
      outflow_datasize: '响应包大小',
      attack_info: {
        vulntype: '攻击类型',
        description: '攻击类型的描述',
        attack_detail: '攻击详情'
      },
      scan_info: {
        scan_tool: '扫描工具',
        scan_positon: '扫描位置',
        description: '扫描工具描述',
        scan_detail: '扫描详情'
      },
      conf_info: {
        appname: '应用名称',
        protocol: '协议类型',
        domain: '防护域名',
        check_point: '检查点',
        description: '描述',
        username: '用户名'
      }
    }
    for (let key in this.data) {
      if (key == 'attack_info') {
        var attack_info = {}
        for (let i in this.data[key]) {
          attack_info[bible.attack_info[i]] = this.data.attack_info[i]
        }
        this.attack_block = true
        this.attack_info = attack_info
      } else if (key == 'scan_info') {
        var scan_info = {}
        for (let i in this.data[key]) {
          scan_info[bible.scan_info[i]] = this.data.scan_info[i]
        }
        this.scan_block = true
        this.scan_info = scan_info
      } else if (key == 'conf_info') {
        var conf_info = {}
        for (let i in this.data[key]) {
          conf_info[bible.conf_info[i]] = this.data.conf_info[i]
        }
        this.conf_block = true
        this.conf_info = conf_info
      } else {
        this.basic_data[bible[key]] = this.data[key]
      }
    }
  },
  methods: {}
}
</script>
<style scoped>
ul,
li {
  list-style: none;
  margin: 10px;
}
</style>
