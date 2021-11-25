<template>
  <div class="employee-events">
    <div class="employee-events__item">
      <div class="employee-events__item-num">
        {{ eventsLength }}
      </div>
      <div class="employee-events__item-text">
        поездки
      </div>
    </div>
    <div class="employee-events__item">
      <div class="employee-events__item-num">
        {{ eventsCounter }}
      </div>
      <div class="employee-events__item-text">
        дней коммандировки
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    userId: {
      type: String,
      required: true
    },
    users: {
      type: Array,
      required: true
    }
  },
  computed: {
    eventsLength () {
      if (!this.$root.selectedUser) return
      return this.users.find(user => user.id === this.userId).eventList.length
    },
    eventsCounter () {
      if (!this.$root.selectedUser) return
      return this.users
        .find(user => user.id === this.userId)
        .eventList.map(item => item.dates)
        .flat(Infinity).length
    }
  }
}
</script>

<style lang="scss" scoped>
.employee-events {
  padding: 2.31rem 1.875rem 0.56rem;
  &__item {
    padding: 0.69rem 0;
    display: flex;
    align-items: center;
    justify-content: space-between;
    &:not(:last-child) {
      border-bottom: 1px solid rgba(#000, 0.1);
    }

    &-num {
      font-size: 2rem;
    }
  }
}
</style>
