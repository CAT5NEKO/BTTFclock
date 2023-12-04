<template>
  <div id="clock">
    <div class="time-container">
      <h1 :style="{ color: futureDateColor, backgroundColor: 'black' }" id="future-date">{{ futureDate }}</h1>
      <p>DESTINATION TIME</p>
    </div>
    <div class="time-container">
      <h1 :style="{ color: currentDateColor, backgroundColor: 'black' }" id="current-date">{{ currentDate }}</h1>
      <p>PRESENT TIME</p>
    </div>
    <div class="time-container">
      <h1 :style="{ color: pastDateColor, backgroundColor: 'black' }" id="past-date">{{ pastDate }}</h1>
      <p>LAST TIME DEPARTED</p>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      currentDate: '',
      pastDate: '',
      futureDate: '',
      currentDateColor: 'yellow',
      pastDateColor: 'red',
      futureDateColor: 'green',
      previousFutureDate: null //過去に未来だった日付けを貯めておく場所
    };
  },
  mounted() {
    this.updateClock();
    setInterval(this.updateClock, 2000);　//本来ならプルトニウムは有限だしドクはこんなに時間弄らないけどコロコロ変わった方が面白い
  },
  methods: {
    getRandomDate(start, end) {
      const startTimestamp = start.getTime();
      const endTimestamp = end.getTime();
      const range = endTimestamp - startTimestamp;
      const randomOffset = Math.floor(Math.random() * range);
      const randomTimestamp = startTimestamp + randomOffset;
      return new Date(randomTimestamp);
    },
    updateClock() {
      const currentDateTime = new Date();
      let pastDateTime = this.previousFutureDate || this.getRandomDate(new Date('1950-01-01T00:00:00'), new Date('1985-11-05T01:21:00'));
      const futureDateTime = this.getRandomDate(new Date('1950-01-01T00:00:00'), new Date('1985-11-05T01:21:00'));
      this.currentDate = this.formatDate(currentDateTime);
      this.pastDate = this.formatDate(pastDateTime);
      this.futureDate = this.formatDate(futureDateTime);
      this.previousFutureDate = futureDateTime;
    },
    formatDate(date) {
      const months = ['JAN', 'FEB', 'MAR', 'APR', 'MAY', 'JUN', 'JUL', 'AUG', 'SEP', 'OCT', 'NOV', 'DEC'];
      const month = months[date.getMonth()];
      const day = date.getDate().toString().padStart(2, '0');
      const year = date.getFullYear();
      const hours = date.getHours().toString().padStart(2, '0');
      const minutes = date.getMinutes().toString().padStart(2, '0');

      return `${month} ${day} ${year} ${hours}:${minutes}`;
    }
  }
};
</script>

<style scoped>
#clock {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-around;
  font-size: 2em;
  text-align: center;
  padding: 20px;
  background-color: #23232a;
  color: #cdcdde;
}

.time-container {
  margin-bottom: auto;
  padding: 10px;
}

h1 {
  margin: 0;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
  width: 100%;
  font-family: "Arial Black";

}

p {
  margin: 5px 0 0;
  font-family: 'Arial Black';
  text-align: center;
  text-overflow: ellipsis;
}
</style>