<template>
  <q-page padding class="row justify-center">
    <q-card style="max-width: 600px; width: 100%;">
      <q-card-section>
        <div class="text-h6">Basic Contact Form</div>
      </q-card-section>

      <q-card-section>
        <q-form @submit.prevent="onSubmit" ref="formRef">
          <q-input v-model="form.name" label="Name" lazy-rules :rules="[val => !!val || 'Name is required']" />
          <q-input v-model="form.email" label="Email" type="email" lazy-rules :rules="[val => !!val || 'Email is required']" />
          <q-select
            v-model="form.topic"
            :options="['Question','Feedback','Other']"
            label="Topic"
          />
          <q-input v-model="form.message" type="textarea" label="Message" autogrow />
          <div class="row q-mt-md">
            <q-btn label="Submit" type="submit" />
            <q-btn flat label="Reset" @click="resetForm" class="q-ml-sm" />
          </div>
        </q-form>
      </q-card-section>
    </q-card>
  </q-page>
</template>

<script setup>
import { ref } from 'vue'
import { useQuasar } from 'quasar'

const $q = useQuasar()
const formRef = ref(null)
const form = ref({
  name: 'Kuriya thathe',
  email: 'kuriya122thathe@gmail.com',
  topic: 'Question',
  message: 'thank you kuriya'
})

function resetForm () {
  form.value = { name: '', email: '', topic: 'Question', message: '' }
  formRef.value && formRef.value.resetValidation && formRef.value.resetValidation()
}

function onSubmit () {
  // ตัวอย่างใช้ Notify เพื่อแจ้งผล -- จะต้องเปิด plugin Notify ใน quasar.config.js (ขั้นตอนถัดไป)
  $q.notify({
    type: 'positive',
    message: `Thanks ${form.value.name}! We received your ${form.value.topic}.`
  })
  // ทำเป็นแค่ตัวอย่าง — จะไม่ส่งข้อมูลจริง
}
</script>

<style scoped>
/* ปรับแต่งเล็กน้อยถ้าต้องการ */
</style>
