<script setup lang="ts">
const tickets = ref(JSON.parse(localStorage.getItem('tickets')))

const updateStatus = updatedTicket => {
  const index = tickets.value.findIndex(ticket => ticket.ticketNumber === updatedTicket.ticketNumber)

  if (index !== -1) {
    tickets.value[index].isCompleted = !updatedTicket.ticketStatus
    localStorage.setItem('tickets', JSON.stringify(tickets.value))
    console.log(tickets)
  }
}
</script>

<template>
  <div>
    <VRow>
      <VCol
        v-for="item in tickets"
        :key="item"
        cols="12"
        md="4"
      >
        <TicketEntry
          :ticket-number="item.ticketNumber"
          :name="item.name"
          :department="item.department"
          :issue="item.issue"
          :description="item.description"
          :completed="item.isCompleted"
          @change-status="updateStatus"
        />
      </VCol>
    </VRow>
  </div>
</template>
