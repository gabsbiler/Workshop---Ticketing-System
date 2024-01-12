<script setup lang="ts">
import { ref } from 'vue'

const form = ref({
  name: '',
  issue: '',
  department: '',
  description: [],
  isCompleted: false,
})

const problemField = ref()

const addProblem = () => {
  form.value.description.push(problemField.value)
  problemField.value = ''
}

const addTicket = () => {
  const now = new Date()

  const ticketNumber = `${(now.getMonth() + 1).toString().padStart(2, '0')
  }${now.getDate().toString().padStart(2, '0')}-${
    now.getHours().toString().padStart(2, '0')
  }${now.getMinutes().toString().padStart(2, '0')
  }${now.getSeconds().toString().padStart(2, '0')}`

  const newTicket = { ...form.value, ticketNumber }
  const tickets = JSON.parse(localStorage.getItem('tickets') || '[]')

  tickets.push(newTicket)

  localStorage.setItem('tickets', JSON.stringify(tickets))

  form.value = { name: '', issue: '', department: '', description: [] }
}
</script>

<template>
  <div class="d-flex justify-center">
    <VCard
      title="Request Form"
      style="inline-size: 45rem;"
    >
      <VCardText>
        <VForm>
          <VRow>
            <VCol cols="12">
              <VTextField
                v-model="form.name"
                label="Name"
              />
            </VCol>
            <VCol cols="12">
              <VTextarea
                v-model="form.issue"
                label="Issue"
              />
            </VCol>
            <VCol cols="12">
              <VTextField
                v-model="form.department"
                label="Department"
              />
            </VCol>
          </VRow>

          <VRow>
            <VCol>
              <h6 class="text-h6">
                List problems:
              </h6>
              <h6
                v-for="problem in form.description"
                :key="problem"
                class="text-h6"
              >
                &nbsp; <VIcon icon="ri-arrow-right-double-line" />{{ problem }}
              </h6>
            </VCol>
          </VRow>

          <VRow>
            <VCol class="d-flex align-center gap-x-3">
              <VTextField
                v-model="problemField"
                label="Enter Problem"
              />
              <VBtn @click="addProblem">
                Add
              </VBtn>
            </VCol>
          </VRow>

          <VRow>
            <VCol>
              <VBtn
                block
                @click="addTicket"
              >
                Save
              </VBtn>
            </VCol>
          </VRow>
        </VForm>
      </VCardText>
    </VCard>
  </div>
</template>
