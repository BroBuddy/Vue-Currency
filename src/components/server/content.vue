<template>
<div class="row">
  <div class="col-xs-12 col-md-4">
      <div class="card">
        <h4 class="card-header">
          Settings
        </h4>
        <div class="card-block">
          <table class="table table-striped">
          <thead>
              <tr>
                <th>Option</th>
                <th>Value</th>
            </tr>
          </thead>
          <tbody>
            <tr>
              <td>Year</td>
              <td>
                <select v-model="year" @change="changeAPI(base)">
                  <option v-for="year in 20">{{ year+1998 }}</option>
                </select>
              </td>
            </tr>
            <tr>
              <td>Month</td>
              <td>
                <select v-model="month" @change="changeAPI(base)">
                  <option v-for="month in months">{{ month }}</option>
                </select>
              </td>
            </tr>
            <tr>
              <td>Day</td>
              <td>
                <select v-model="day" @change="changeAPI(base)">
                  <option v-for="day in days">{{ day }}</option>
                </select>
              </td>
            </tr>
            <tr>
              <td>Currency</td>
              <td>
                1 {{ base }}
                <img :src="getImage(base)" alt="" />
              </td>
            </tr>
          </tbody>
          </table>
        </div>
      </div>
    </div>

    <div class="col-xs-12 col-md-8">
      <div class="card">
        <h4 class="card-header">
          Exchange Rates
        </h4>
        <div class="card-block">
          <table class="table table-striped">
            <thead>
              <tr>
                <th>Icon</th>
                <th>Name</th>
                <th>Value</th>
                <th>Change</th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="(rate, key, index) in rates">
                <td><img :src="getImage(key)" alt="" /></td>
                <td>{{ key }}</td>
                <td>{{ rate }}</td>
                <td><button class="btn btn-danger" @click="changeAPI(key)">Change</button></td>
              </tr>
            </tbody>
          </table>
        </div>
      </div>
  </div>
</div>
</template>

<script>
export default {
  data: function() {
    return {
        base: '',
        date: '',
        year: '',
        month: '',
        day: '',
        months: ['01', '02', '03', '04', '05', '06', '07', '08', '09', '10', '11', '12'],
        days: ['01', '02', '03', '04', '05', '06', '07', '08', '09', '10', '11', '12', '13', '14', '15', '16', '17', '18', '19', '20', '21', '22', '23', '24', '25', '26', '27', '28', '29', '30', '31'],
        rates: []
    }
  },
  created: function() {
  	this.$http.get('https://api.fixer.io/latest').then(function(response) {
  		this.base = response.body.base;
  		this.date = response.body.date;
        this.rates = response.body.rates;
        this.year = this.date.split('-')[0];
        this.month = this.date.split('-')[1];
        this.day = this.date.split('-')[2];
    });
  },
  methods: {
    getImage: function(key) {
        return 'http://fxtop.com/ico/' + key + '.gif';
    },
    changeAPI: function(key) {
    	if (this.month.length === 1) {
            this.month = '0' + this.month;
        }
        
        if (this.day.length === 1) {
            this.day = '0' + this.day;
        }
        
        var url = 'https://api.fixer.io/' + this.year + '-' + this.month + '-' + this.day + '?base=' + key;
        
        this.$http.get(url).then(function(response) {
            this.base = response.body.base;
            this.date = response.body.date;
            this.rates = response.body.rates;
        });
    }
  }
}
</script>

<style lang="scss" scoped>
</style>
