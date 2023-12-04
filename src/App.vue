<template>
  <div id="clock">
    <h1 id="current-date">{{ currentDate }}</h1>
    <h1 id="past-date">{{ pastDate }}</h1>
    <h1 id="future-date">{{ futureDate }}</h1>
  </div>
</template>

<script>
export default {
  data() {
    return {
      currentDate: '',
      pastDate: '',
      futureDate: ''
    };
  },
  mounted() {
    this.updateClock();
    setInterval(this.updateClock, 1000);
  },
  methods: {
    getRandomDate(start, end) {
      return new Date(start.getTime() + Math.random() * (end.getTime() - start.getTime()));
    },
    updateClock() {
      const currentDateTime = new Date();
      const pastDateTimeStart = new Date('1950-01-01T00:00:00');
      const pastDateTimeEnd = new Date('1985-11-05T01:21:00');
      const futureDateTimeStart = new Date('1955-11-05T01:21:00');
      const futureDateTimeEnd = new Date('2050-01-01T00:00:00');

      const pastDateTime = this.getRandomDate(pastDateTimeStart, pastDateTimeEnd);
      const futureDateTime = this.getRandomDate(futureDateTimeStart, futureDateTimeEnd);

      this.currentDate = this.formatDate(currentDateTime);
      this.pastDate = this.formatDate(pastDateTime);
      this.futureDate = this.formatDate(futureDateTime);
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
  font-size: 2em;
  text-align: center;
  border: 5px solid #fff;
  padding: 20px;
  border-radius: 10px;
}

#clock h1 {
  margin: 0;
  font-size: 1.5em;
}

#clock #current-date {
  color: red;
}

#clock #past-date {
  color: yellow;
}

#clock #future-date {
  color: green;
}
</style>
