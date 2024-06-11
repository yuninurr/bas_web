<script setup>
import { VNumberInput } from 'Vuetify/labs/VNumberInput'
import { inject, reactive } from 'vue'

const formData = reactive({
  AccountId: '',
  BankId: '',
  Amount: 0,
  TransactionDate: '',
  pesanLogin: ''
})

const myAxios = inject('myAxios')

const handleSubmit = () => {
  console.log('login clicked', formData)

  myAxios.post('/transaction/transfer-bank', formData).then(
    (res) => {
      if (res.status == 200) {
        formData.pesanLogin = 'Anda berhasil submit transaksi'
      }
      formData.snackbar = true
      // eslint-disable-next-line no-unused-vars
    },
    (err) => {
      formData.pesanLogin = 'Anda gagal transaksi'
      formData.snackbar = true
    }
  )
}
</script>

<template>
  <v-card variant="tonal" class="pa-5">
    <div class="container">
      <div>
        <label>AccountID</label>
        <v-text-field type="text" v-model="formData.AccountId" />
      </div>
      <div>
        <label>BankID</label>
        <v-text-field type="text" v-model="formData.BankId" />
      </div>

      <div>
        <label>Amount</label>
        <v-number-input v-model="formData.Amount" />
      </div>

      <div>
        <label>TransactionDate</label>
        <v-text-field id="TransactionDate" v-model="formData.TransactionDate" />
      </div>
      <v-btn variant="tonal" @click="handleSubmit"> Submit </v-btn>
      <v-snackbar v-model="formData.snackbar">
        {{ formData.pesanLogin }}
        <template v-slot:actions>
          <v-btn
            color="black"
            variant="text"
            @click="formData.snackbar = false"
            style="text-transform: none"
          >
            Close
          </v-btn>
        </template>
      </v-snackbar>
    </div>
  </v-card>
</template>
