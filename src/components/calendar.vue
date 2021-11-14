<template>
  <div class="calendar">
    <div class="calendar-wrapper">
      <v-calendar
        class="calendar-component"
        :masks="masks"
        :from-page="{ month: 6, year: 2021 }"
        is-expanded
        title-position="left"
      >
      </v-calendar>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    // const month = new Date().getMonth()
    // const year = new Date().getFullYear()
    return {
      masks: {
        weekdays: 'WWWW'
      }
    }
  }
}
</script>

<style lang="scss">
// @import "../assets/styles/typography.scss";

.calendar-wrapper {
  padding: 1.1875rem 1.625rem 4.1875rem;
  background: #fff;
  min-height: 40.875rem;
  border-radius: 0.44rem;
}

.calendar-component.vc-container {
  font-family: "RobotoCondensed";
  text-transform: capitalize;
  width: 100%;
  border: none;

  --border: 1px solid #e9e9e9;

  --day-width: 7.62rem;
  --day-height: 5.57rem;

  & .vc-header {
    margin-bottom: 2.08rem;
    padding-left: 0;
    padding-bottom: 2.885rem;
    border-bottom: 2px solid rgba(0, 65, 102, 0.1);
  }
  & .vc-title {
    font-size: 2rem;
    font-weight: var(--font-bold);
  }
  & .vc-arrows-container {
    justify-content: flex-end;
  }

  & .vc-arrow {
    width: 2.21rem;
    height: 2.21rem;
    border-radius: 100%;
    background: rgba(0, 66, 105, 0.07);
    &:not(:last-child) {
      margin-right: 0.33rem;
    }
    &:hover {
      background: #0078d2;
      & .vc-svg-icon path {
        color: #fff;
      }
    }
  }

  & .vc-weeks {
    padding: 0;
    border-left: var(--border);
  }

  & .vc-weekday {
    margin-left: -1px;
    text-align: left;
    font-size: 0.75rem;
    color: #000;
    background: #fff;
    border-bottom: var(--border);
  }

  & .vc-day {
    padding: 0.44rem 0.44rem 0.56rem;

    justify-content: flex-end;
    align-items: flex-start;

    // min-width: var(--day-width);
    min-height: var(--day-height);

    text-align: right;
    border-right: var(--border);
    border-bottom: var(--border);
  }

  & .vc-day.weekday-position-6,
  .vc-day.weekday-position-7 {
    background: #fcfcfc;
  }
  & .vc-day.is-not-in-month * {
    opacity: 1;
    color: #c0c3cc;
  }

  .vc-day-content {
    font-size: 1rem;
  }
}
</style>
