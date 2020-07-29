<template>
  <div class="container main-w">
    <div>
      <el-tabs>
        <!-- 转账USDT -->
        <el-tab-pane label="转账ERC20">
          <el-form ref="tokenForm" :model="tokenForm" label-width="150px">
            <el-form-item label="from" prop="from">
              <el-input v-model="tokenForm.from"></el-input>
            </el-form-item>
            <el-form-item label="privateKey" prop="privateKey">
              <el-input v-model="tokenForm.privateKey"></el-input>
            </el-form-item>
            <el-form-item label="to" prop="to">
              <el-input v-model="tokenForm.to"></el-input>
            </el-form-item>
            <el-form-item label="contractAddress" prop="contractAddress">
              <el-input v-model="tokenForm.contractAddress"></el-input>
            </el-form-item>
            <el-form-item label="abi" prop="abi">
              <el-input v-model="tokenForm.abi" type="textarea" :rows="4"></el-input>
            </el-form-item>
            <el-form-item>
              <div class="btns">
                <el-button type="primary" @click="handleTransferUSDT()">转账</el-button>
                <el-button type="danger" @click="handleReset('tokenForm')">重置</el-button>
              </div>
            </el-form-item>
          </el-form>
        </el-tab-pane>

        <!-- 转账ETH -->
        <el-tab-pane label="转账ETH">
          <el-form ref="ethForm" :model="ethForm" label-width="150px">
            <el-form-item label="from" prop="from">
              <el-input v-model="ethForm.from"></el-input>
            </el-form-item>
            <el-form-item label="privateKey" prop="privateKey">
              <el-input v-model="ethForm.privateKey"></el-input>
            </el-form-item>
            <el-form-item label="to" prop="to">
              <el-input v-model="ethForm.to"></el-input>
            </el-form-item>
            <el-form-item>
              <div class="btns">
                <el-button type="primary" @click="handleTransferETH()">转账</el-button>
                <el-button type="danger" @click="handleReset('ethForm')">重置</el-button>
              </div>
            </el-form-item>
          </el-form>
        </el-tab-pane>
      </el-tabs>
    </div>
  </div>
</template>

<script>
import ABI from './ABI'
const TransferSDK = window.TransferSDK
const SDK = new TransferSDK('ropsten')

export default {
  data () {
    return {
      tokenForm: {
        from: '',
        to: '',
        value: '',
        contractAddress: '',
        abi: '',
        privateKey: ''
      },
      ethForm: {
        from: '',
        to: '',
        value: '',
        privateKey: ''
      }
    }
  },
  methods: {
    async handleTransferUSDT () {
      try {
        let result = await SDK.transferUSDT(this.tokenForm)
        console.log({result})
      } catch (error) {
        console.log({error})
      }
    },
    async handleTransferETH () {
      try {
        let result = await SDK.transferETH(this.ethForm)
        console.log({result})
      } catch (error) {
        console.log({error})
      }
    },
    handleReset (formName) {
      this.$refs[formName].resetFields()
    }
  },
}
</script>

<style>
.main-w {
  width: 1200px;
}
.container {
  margin: 0 auto;
  padding: 30px;
  display: flex;
  align-items: center;
  justify-content: center;
}
.el-input {
  width: 500px;
}
.btns {
  display: flex;
  justify-content: center;
}
</style>
