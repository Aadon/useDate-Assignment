<template>
  <div class="container">
    <h3>Date: {{ date.toString() }}</h3>

   <h3>Day: {{ getDay() }}</h3>
   
   <h3>Month: {{ getMonth() }}</h3>

    <div class="day">
      <label>Days to Add:</label>
    <input type="number" v-model="daysToAdd" />
    </div>

    <div class="month">
      <label>Months to Add:</label>
    <input type="number" v-model="monthsToAdd" />
    </div>

    <p>
      Added Day: {{ addedDay.toString() }}
      Added Month: {{ addedMonth.toString() }}
    </p>
    
    
  </div>
</template>

<script>
export default {
  data() {
    return {
      date: new Date(),
      daysToAdd: 0,
      monthsToAdd: 0,
    };
  },
  computed: {
    addedDay() {
      return this.addDay(this.daysToAdd).toString();
    },
    addedMonth() {
      return this.addMonth(this.monthsToAdd).toString();
    },
  },
  methods: {
    getDay() {
      return this.date.getDate();
    },
    getMonth() {
      return this.date.getMonth();
    },
    addDay(numberOfDays) {
      const newDate = new Date(this.date.getTime());
      newDate.setDate(newDate.getDate() + numberOfDays);

      if (newDate.getMonth() !== this.date.getMonth()) {
        newDate.setDate(1);
        newDate.setMonth(newDate.getMonth() + 1);
      }

      return newDate;
    },
    addMonth(numberOfMonths) {
      const newDate = new Date(this.date.getTime());
      newDate.setMonth(newDate.getMonth() + numberOfMonths);

      if (newDate.getMonth() > 11) {
        newDate.setFullYear(newDate.getFullYear() + 1);
        newDate.setMonth(0);
      }

      return newDate;
    },
  },
};
</script>

<style scoped>
.container {
  width: 640px;
  margin: 40px auto;
  padding: 20px;
  background-color: #000;
  font-family: sans-serif;
  font-size: 16px;
  color: #d9ebe2;
  border-radius: 8px;
}
h3 {
  display: block;

}
.day, .month {
  margin-bottom: 12px;
} 
label {
  display: block;
  margin-bottom: 5px;
  font-size: 18px;
}
input {
  padding: 6px 10px;
  border: none;
  border-radius: 10px;
  font-size: 16px;
  outline: none;
}
p {
  padding: 6px 0;
  line-height: 28px;
}
</style>