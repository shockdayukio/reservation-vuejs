<template>
  <div>
    <h2>予約一覧</h2>
    <p>
      <button @click="movePreviousWeek">前の1週間</button>
      <strong>{{startDate.format('MM')}}月</strong>
      <button @click="moveNextWeek">後の1週間</button>
    </p>
    <table border="1" align="center">
      <thead>
        <tr>
          <td></td>
          <template v-for="date in dateList">
            <th :key="date">
              {{ date }}
            </th>
          </template>
        </tr>
      </thead>
      <tbody>
        <template v-for="hourlyWorkList in hourlyWorkList">
          <tr :key="hourlyWorkList.time">
            <td>{{hourlyWorkList.time}}</td>
            <td v-for="(work, i) in hourlyWorkList.workList" :key="hourlyWorkList.time + '_' + i">
              <a @click="sendReservation(dateList[i], hourlyWorkList.time, work)">{{work}}</a>
            </td>
          </tr>
        </template>
      </tbody>
    </table>
    <hr>
  </div>
</template>

<script>
  import moment from 'moment'
  export default {
    data(){
      return {
        dateList: [],
        weekNumber: 7,
        hourlyWorkList: []
      }
    },
    created() {
      this.setDateList(this.startDate)
      this.setHourlyWorkList()
    },
    computed: {
      startDate: {
        get() {
          return moment()
        },
        set(date) {
          this.setDateList(date)
          this.setHourlyWorkList()
        }
      }
    },
    methods: {
      moveNextWeek() {
        this.startDate = this.startDate.add(this.weekNumber, 'day')
      },
      movePreviousWeek() {
        this.startDate = this.startDate.subtract(this.weekNumber, 'day')
      },
      setDateList() {
        var dateListClone = this.dateList
        dateListClone = []
        var date = moment(this.startDate)
        dateListClone.push(date.format('DDdd'))
        for (  var i = 0;  i < (this.weekNumber - 1);  i++  ) {
          dateListClone.push(date.add(1, 'day').format('DDdd'))
        }
        this.dateList = dateListClone
      },
      //ダミーデータ用
      getRandomInt(max) {
        // ランダムな配列
        return Math.floor(Math.random() * Math.floor(max));
      },
      setWorkList() {
        //ダミー配列データ生成
        var array = [];
        var max = 2;
        for (let i = 0; i < this.weekNumber; i++) {
          array.push(this.getRandomInt(max));
        }
        return array
      },
      setHourlyWorkList() {
        this.hourlyWorkList = [
          {
            time: "11:00" ,
            workList: this.setWorkList()
          },
          {
            time: "12:00" ,
            workList: this.setWorkList()
          },
          {
            time: "13:00" ,
            workList: this.setWorkList()
        }]
      }
      ,
      sendReservation(date, time, work) {
        this.$emit("send-reservation", date + time + work)//一旦startDate
      }
    }
  };
</script>