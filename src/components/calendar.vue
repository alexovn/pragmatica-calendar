<template>
  <div class="calendar">
    <div class="calendar-wrapper">
      {{dataNotWorkingDays}}
      <v-calendar
        class="calendar-component"
        :masks="masks"
        ref="calendar"
        :attributes="dataArray"
        :from-page="{ month: 6, year: 2021 }"
        is-expanded
        title-position="left"
      >
        <template v-slot:day-content="{ day, attributes }">
          <div class="day-box">
            <span>{{ day.day }}</span>
            <div>
              <p
                v-for="attr in attributes"
                :key="attr.key"
                :style="{backgroundColor: attr.customData.color}"
                class="bubble"
              >
                {{ isHoliday(day.id) ? dataHolidays[0].customData.label : attr.customData.label }}
              </p>
            </div>
          </div>
        </template>
      </v-calendar>
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
    userId: {
      type: String,
      required: true
    }
  },
  data () {
    return {
      masks: {
        weekdays: 'WWWW'
      },
      dataWeekends: [
        {
          customData: {
            label: 'Выходной',
            color: '#97B2C4'
          },
          dates: {
            weekdays: [1, 7]
          }
        }
      ],
      dataHolidays: [
        {
          customData: {
            label: 'Праздник',
            color: '#97B2C4'
          },
          dates: ['2021-06-15', '2021-06-11', '2021-06-12']
        }
      ]
    }
  },
  methods: {
    isHoliday (isoDate) {
      return this.dataHolidays[0].dates.includes(isoDate)
    },
    isWeekday (day) {
      return new Date(Date.parse(day)).getDay()
    }
  },
  computed: {
    dataAttributes () {
      if (!this.userId) return
      return this.users
        .find(user => user.id === this.userId)
        .eventList.map(item => ({
          customData: {
            label: item.city,
            color: item.cityColor
          },
          dates: item.dates
        }))
    },
    dataArray () {
      return [...this.dataAttributes, ...this.dataNotWorkingDays]
    },
    clearHolidays () {
      const clearDates = this.dataHolidays[0].dates.filter(date => {
        return this.isWeekday(date) !== 6 && this.isWeekday(date) !== 0
      })
      return clearDates
    },
    dataNotWorkingDays () {
      const newHolidays = [
        {
          customData: this.dataHolidays[0].customData,
          dates: this.clearHolidays
        }
      ]
      return [...this.dataWeekends, ...newHolidays]
    }
  }
}
</script>

<style lang="scss">
.bubble {
  padding: 0.3rem 0.4rem;
  min-height: 1.24rem;
  font-size: 0.75rem;
  text-align: center;
  color: #fff;
  border-radius: 4px;
}

.day-box {
  display: flex;
  flex-direction: column;
  span {
    height: 100%;
  }
}

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
    display: flex;
    justify-content: flex-end;

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

    .bubble {
      color: #fff;
    }
  }

  .vc-day-content {
    font-size: 1rem;
  }
}
</style>
