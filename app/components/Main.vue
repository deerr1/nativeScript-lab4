<template>
  <Page>
    <ActionBar>
      <Label text="Календарь" />
    </ActionBar>

    <FlexboxLayout flexDirection="column" justifyContent="start">
      <FlexboxLayout
        flexDirection="row"
        justifyContent="space-between"
        alignItems="center"
        class="header"
      >
        <Label
          :text="date.getFullYear() + ' ' + months[date.getMonth()]"
          textAlignment="center"
          class="date"
        />
        <StackLayout orientation="horizontal">
          <Button text="<" @tap="minusMonth" class="button" />
          <Button text=">" @tap="plusMonth" class="button" />
        </StackLayout>
      </FlexboxLayout>
      <Calendary
        class="box"
        :month="date.getMonth()"
        :year="date.getFullYear()"
        :today="today.toDateString()"
        :key="date.getMonth()"
      />
      <AbsoluteLayout v-if="today.toDateString() !== date.toDateString()">
          <Button :text="today.getDate()" @tap="reset" left="280" class="btnReset" />
      </AbsoluteLayout>
    </FlexboxLayout>
  </Page>
</template>

<script>
import Calendary from "~/components/Calendary.vue";
export default {
  components: {
    Calendary,
  },
  data: function () {
    return {
      today: new Date(),
      date: new Date(),
      months: [
        "Январь",
        "Февраль",
        "Март",
        "Апрель",
        "Май",
        "Июнь",
        "Июль",
        "Август",
        "Сентябрь",
        "Октябрь",
        "Ноябрь",
        "Декабрь",
      ],
    };
  },
  methods: {
    plusMonth() {
      this.date = new Date(this.date.setMonth(this.date.getMonth() + 1));
    },
    minusMonth() {
      this.date = new Date(this.date.setMonth(this.date.getMonth() - 1));
    },
    reset() {
        this.date = new Date()
    }
  },
};
</script>

<style scoped lang="scss">
.box {
  width: 100%;
  height: 50%;
}
.header {
  margin: 1%, 0, 3%, 2%;
}
.date {
  font-size: 20vw;
}
.button {
  vertical-align: center;
  border-radius: 20%;
  font-size: 20wv;
  width: 35wv;
  height: 35wv;
  color: white;
  background-color: rgb(115, 115, 255);
}
.btnReset {
  border-radius: 30%;
  font-size: 20wv;
  width: 50wv;
  height: 50wv;
  color: white;
  background-color: rgb(115, 115, 255);
}
</style>
