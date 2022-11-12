<template>
  <div class="testUSDW">
    <div class="header">
      <ConnectWallet></ConnectWallet>
    </div>
    <h2>查询方法</h2>
    <div class="row">
      <el-col>代币总供应量(_totalSupply)</el-col>
      <el-col><el-button @click="_totalSupply">TotalSupply</el-button></el-col>
      <el-col>{{ totalSupply }}</el-col>
    </div>
    <div class="row">
      <el-col>余额查询(balanceOf)</el-col>
      <el-input v-model="search1" placeholder="查询对象地址"></el-input>
      <el-col><el-button @click="balanceOf">balanceOf</el-button></el-col>
      <el-col>{{ balance }}</el-col>
    </div>
    <h2>基本调用</h2>
    <el-aside width="200px">
      <strong> 1Approve</strong>
    </el-aside>
    <el-container>
      <el-header>
        <strong>授权此代币</strong>
      </el-header>
      <el-main>
        <el-input v-model="input1" placeholder="授权对象地址"></el-input>
        <el-input v-model="input2" placeholder="授权金额"></el-input>
        <el-button @click="approve">Approve</el-button>
      </el-main>
    </el-container>
    <el-aside width="200px">
      <strong>2Transfer</strong>
    </el-aside>
    <el-container>
      <el-header>
        <strong>转移此代币</strong>
      </el-header>
      <el-main>
        <el-input v-model="input3" placeholder="转给谁"></el-input>
        <el-input v-model="input4" placeholder="金额"></el-input>
        <el-button @click="transfer">Transfer</el-button>
      </el-main>
    </el-container>
    <el-aside width="200px">
      <strong>3pause</strong>
    </el-aside>
    <el-container>
      <el-header>
        <strong>暂停交易</strong>
      </el-header>
      <el-main>
        <el-button @click="pause">pause</el-button>
      </el-main>
    </el-container>
    <el-aside width="200px">
      <strong>4addBlackList</strong>
    </el-aside>
    <el-container>
      <el-header>
        <strong>添加黑名单成员</strong>
      </el-header>
      <el-main>
        <el-input v-model="input5" placeholder="地址"></el-input>
        <el-button @click="addBlackList">addBlackList</el-button>
      </el-main>
    </el-container>
    <el-aside width="200px">
      <strong>5transferOwnership</strong>
    </el-aside>
    <el-container>
      <el-header>
        <strong>转让管理员</strong>
      </el-header>
      <el-main>
        <el-input v-model="input6" placeholder="地址"></el-input>
        <el-button @click="transferOwnership">transferOwnership</el-button>
      </el-main>
    </el-container>
    <el-aside width="200px">
      <strong>6 issue</strong>
    </el-aside>
    <el-container>
      <el-header>
        <strong>增发</strong>
      </el-header>
      <el-main>
        <el-input v-model="input7" placeholder="金额"></el-input>
        <el-button @click=" issue"> issue</el-button>
      </el-main>
    </el-container>
  </div>

</template>

<script>
import ConnectWallet from "../components/ConnectWallet"
export default {
  name: "testUSDW",
  components:{ConnectWallet},
  data() {
    return {
      search1:undefined,
      input1: undefined,
      input2: undefined,
      input3: undefined,
      input4: undefined,
      input5:undefined,
      input6:undefined,
      input7:undefined,
      totalSupply:undefined,
      balance:undefined
    }
  },
  methods:{
    approve(){
      this.$store.dispatch("usdt/approve",{_spender:this.input1,_value:this.input2}).then(res=>{
        console.log(res)
        alert("success")
      }).catch(err=>{
        console.log(err)
        alert("failed")
      })
    },
    transfer(){
      this.$store.dispatch("usdt/approve",{_to:this.input3,_value:this.input4}).then(res=>{
        console.log(res)
        alert("success")
      }).catch(err=>{
        console.log(err)
        alert("failed")
      })
    },
    pause(){
      this.$store.dispatch("usdt/pause",).then(res=>{
        console.log(res)
        alert("success")
      }).catch(err=>{
        console.log(err)
        alert("failed")
      })
    },
    addBlackList(){
      this.$store.dispatch("usdt/addBlackList",this.input5).then(res=>{
        console.log(res)
        alert("success")
      }).catch(err=>{
        console.log(err)
        alert("failed")
      })
    },
    transferOwnership(){
      this.$store.dispatch("usdt/transferOwnership",this.input6).then(res=>{
        console.log(res)
        alert("success")
      }).catch(err=>{
        console.log(err)
        alert("failed")
      })
    },
    issue(){
      this.$store.dispatch("usdt/issue",this.input7).then(res=>{
        console.log(res)
        alert("success")
      }).catch(err=>{
        console.log(err)
        alert("failed")
      })
    },
    _totalSupply(){
      this.$store.dispatch("usdt/_totalSupply").then(res=>{
        this.totalSupply= res
      })
    },
    balanceOf(){
      this.$store.dispatch("usdt/balanceOf",this.search1).then(res=>{
        this.balance= res
      })
    },

  }
}
</script>

<style lang="scss" scoped>
::v-deep .el-input__inner{
  width: 500px;
}
.row{
  display: flex;
  justify-content: space-around;
  padding: 2em 0;
  border-bottom: 2px solid #eee;
}
</style>
