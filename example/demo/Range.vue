<template>
  <div class="box">
    <section>
      <p>date range</p>
      <DatePicker
        v-model="value1"
        type="date"
        :range-separator="' − '"
        :format="'DD.MM.YYYY'"
        :confirm="true"
        :cancel="true"
        range
      >
        <template #sidebar>
          <div class="sidebar">
            <button class="sidebar__button" @click="createRangeDates('today')">here</button>
          </div>
        </template>
      </DatePicker>
    </section>
    <section>
      <p>datetime range</p>
      <date-picker
        v-model="value2"
        type="datetime"
        range
        placeholder="Select datetime range"
      ></date-picker>
    </section>
  </div>
</template>

<script>
import { lastDayOfMonth } from 'date-fns';

export default {
  name: 'Range',
  data() {
    return {
      value1: [new Date(2019, 9, 8), new Date(2019, 9, 19)],
      value2: [],
    };
  },

  methods: {
    createRangeDates(range) {
      const today = new Date();
      switch (range) {
        case 'today': {
          this.value1 = [today, today];
          break;
        }
        case 'yesterday': {
          const yesterday = new Date(today.getFullYear(), today.getMonth(), today.getDate() - 1);

          this.value1 = [yesterday, yesterday];
          break;
        }
        case 'lastWeek': {
          const firstDate = new Date(today.getFullYear(), today.getMonth(), today.getDate() - 6);
          const lastDate = new Date(today.getFullYear(), today.getMonth(), today.getDate());

          this.value1 = [firstDate, lastDate];
          break;
        }
        case 'last30Days': {
          const firstDate = new Date(today.getFullYear(), today.getMonth(), today.getDate() - 30);
          const lastDate = new Date(today.getFullYear(), today.getMonth(), today.getDate());

          this.value1 = [firstDate, lastDate];
          break;
        }
        case 'thisMonth': {
          const fistDay = new Date(today.getFullYear(), today.getMonth(), 1);
          const lastDay = lastDayOfMonth(fistDay);
          this.value1 = [fistDay, lastDay];
          break;
        }
        case 'lastMonth': {
          const fistDay = new Date(today.getFullYear(), today.getMonth() - 1, 1);
          const lastDay = lastDayOfMonth(fistDay);
          this.value1 = [fistDay, lastDay];
          break;
        }
        default:
          this.value1 = [];
          break;
      }
    },
  },
};
</script>
