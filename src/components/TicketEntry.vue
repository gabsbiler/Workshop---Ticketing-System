<script setup lang="ts">
const props = defineProps(['ticketNumber', 'name', 'department', 'description', 'issue', 'completed'])
const emit = defineEmits(['changeStatus'])

const updateStatus = status => {
  emit('changeStatus', { ticketStatus: status, ticketNumber: props.ticketNumber })
}
</script>

<template>
  <VCard :title="`Ticket No.${props.ticketNumber}`">
    <VCardText>
      <h6 class="text-h6">
        Request By: {{ props.name }} <br>
        Department: {{ props.department }}
      </h6>
      <p class="text-body-2">
        {{ props.issue }}
      </p>
      <h6 class="text-h6">
        Problems:
      </h6>
      <ul class="ms-5">
        <li
          v-for="problem in props.description"
          :key="problem"
        >
          {{ problem }}
        </li>
      </ul>
      <VBtn
        v-if="!completed"
        block
        class="mt-3"
        color="primary"
        @click="updateStatus(props.completed)"
      >
        <VIcon
          icon="ri-checkbox-circle-line"
          start
        />
        Mark as Completed
      </VBtn>
      <VBtn
        v-if="completed"
        block
        class="mt-3"
        color="success"
        @click="updateStatus(props.completed)"
      >
        <VIcon
          icon="ri-checkbox-circle-line"
          start
        />
        Completed
      </VBtn>
    </VCardText>
  </VCard>
</template>
