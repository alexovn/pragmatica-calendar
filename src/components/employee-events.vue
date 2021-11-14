<template>
  <div class="employee-events">
    <div class="employee-events__item">
      <div class="employee-events__item-num">
        4
      </div>
      <div class="employee-events__item-text">
        поездки
      </div>
    </div>
    <div class="employee-events__item">
      <div class="employee-events__item-num">
        9
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
    users: {
      type: Array,
      required: true
    },
    events: {
      type: Array,
      required: true
    }
  },
  data () {
    return {}
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

    &-text {
    }
  }
}
</style>
