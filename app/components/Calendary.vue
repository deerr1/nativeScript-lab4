<template>
  <!-- <FlexLayout >
        <StackLayout v-for="day in days" :key="day">
            <Label :text="day" />
        </StackLayout>
    </FlexLayout> -->
  <GridLayout rows="*, *, *, *, *, *, *" columns="*, *, *, *, *, *, *">
    <Label text="ПН" textAlignment="center" row="0" col="0" />
    <Label text="ВТ" textAlignment="center" row="0" col="1" />
    <Label text="СР" textAlignment="center" row="0" col="2" />
    <Label text="ЧТ" textAlignment="center" row="0" col="3" />
    <Label text="ПТ" textAlignment="center" row="0" col="4" />
    <Label text="СБ" textAlignment="center" row="0" col="5" />
    <Label text="ВС" textAlignment="center" row="0" col="6" />

    <StackLayout
      v-for="(day, index) in days"
      :key="index"
      :row="1 + index / 7"
      :col="index % 7"
      :class="[
        'item',
        !day.isThisMonth ? 'anotherMonth' : '',
        day.isToday ? 'today' : '',
        (1 + index) % 7 == 0 ? 'dayoff' : 'day',
      ]"
    >
      <Label :text="day.date" textAlignment="center" />
    </StackLayout>
  </GridLayout>
</template>

<script>
export default {
  props: ["month", "year", "today"],
  data: function () {
    return {
      days: [{ date: 1, isThisMonth: true, isToday: false }],
    };
  },
  mounted: function () {
    let date = new Date();
    let isToday =
      new Date(this.year, this.month, date.getDate()).toDateString() ==
      date.toDateString();
    let today = date.getDate();

    let days = [];
    for (
      let i = 1;
      i <= new Date(this.year, this.month + 1, 0).getDate();
      i++
    ) {
      if (isToday && i == today) {
        days.push({ date: i, isThisMonth: true, isToday: true });
      } else {
        days.push({ date: i, isThisMonth: true, isToday: false });
      }
    }
    let lastMonth = [];
    let limit = (new Date(this.year, this.month, 1).getDay() + 6) % 7;
    for (let i = 1; i <= limit; i++) {
      lastMonth.unshift({
        date: new Date(this.year, this.month, 1 - i).getDate(),
        isThisMonth: false,
        isToday: false,
      });
    }
    lastMonth = lastMonth.concat(days);
    let nextMonth = [];
    for (let i = 1; i <= 42 - lastMonth.length; i++) {
      nextMonth.push({ date: i, isThisMonth: false, isToday: false });
    }
    this.days = lastMonth.concat(nextMonth);
  },
  methods: {},
};
</script>

<style>
.item {
  font-size: 18vw;
  vertical-align: center;
  margin-bottom: 2%;
  width: 40vw;
  height: 40vw;
}
.day {
  background-color: rgb(219, 219, 219);
  border-radius: 20%;
}
.dayoff {
  background-color: rgb(250, 79, 79);
  border-radius: 20%;
}
.anotherMonth {
  opacity: 0.4;
  background-color: rgb(219, 219, 219);
}
.today {
  color: white;
  background-color: rgb(102, 102, 255);
}
</style>
