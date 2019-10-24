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
          <template v-for="date in dateListFormatted">
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
              <a href="https://camp-fire.jp/projects/view/179275">{{work}}</a>
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
    data: function(){
      return {
        startDate: moment(),
        dateList: [],
        weekNumber: 7,
        hourlyWorkList: [
          {
            time: "11:00" ,
            workList: ["○", "×", "○", "×", "○", "×", "○"]
          },
          {
            time: "12:00" ,
            workList: ["○", "×", "○", "×", "○", "×", "○"]
          },
          {
            time: "13:00" ,
            workList: ["○", "×", "×", "×", "×", "×", "×"]
          }
       ],
      }
    },
    computed: {
      dateListFormatted: function() {
        var dateListClone = this.dateList
        dateListClone = []
        var date = moment(this.startDate)
        dateListClone.push(date.format('DDdd'))
        for (  var i = 0;  i < (this.weekNumber - 1);  i++  ) {
          dateListClone.push(date.add(1, 'day').format('DDdd'))
        }
        return dateListClone
      }
    },
    methods: {
      moveNextWeek: function() {
        var newDate = this.startDate.add(this.weekNumber, 'day')

        //startDateプロパティの値が変われば、dateListの値も変わるようにしたい
        this.$set(this.dateList, 0, newDate)
        this.startDate = newDate

        //ダミーデータ
        this.hourlyWorkList = [
          {
            time: "11:00" ,
            workList: ["×", "○", "×", "○", "×", "○","×" ]
          },
          {
            time: "12:00" ,
            workList: ["×", "×", "×", "×", "×", "×", "×"]
          },
          {
            time: "13:00" ,
            workList: ["○", "×", "○", "×", "○", "×", "○"]
          }
        ]
      },
      movePreviousWeek: function() {
        var newDate = this.startDate.subtract(this.weekNumber, 'day')

        //startDateプロパティの値が変われば、dateListの値も変わるようにしたい
        this.$set(this.dateList, 0, newDate)

        //ダミーデータ。上に同じ。
        this.hourlyWorkList = [
          {
            time: "11:00" ,
            workList: ["○", "×", "×", "×", "○", "×", "○"]
          },
          {
            time: "12:00" ,
            workList: ["×", "×", "○", "×", "×", "×", "○"]
          },
          {
            time: "13:00" ,
            workList: ["×", "×", "×", "×", "×", "×", "×"]
          }
        ]
      },
      replaceWorkList: function() {
        //startDateを開始日として、1週間分のhourlyWorkListの内容を再取得内容を再取得再代入
        //returnで返す
      }
    }
  }
</script>