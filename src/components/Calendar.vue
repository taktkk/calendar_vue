<script setup>
import { ref , reactive, computed , onMounted} from "vue" 
  const weekdays = ref(['日','月','火','水','木','金','土'])
  const year = ref(2022)
  const month = ref(10)
  const today = ref('')
  
   
  const calendar = computed(() => {
    let calendar = [];
          let firstWeekDay = new Date(year.value, month.value - 1,1).getDay();
          let lastDay = new Date(year.value, month.value,0).getDate();
          let dayNumber = 1;
          while(dayNumber <= lastDay){
              let weekData = [];
              for(let i = 0;i <= 6;i ++){
                  if(calendar.length == 0 && i < firstWeekDay){
                      weekData[i] = '';
                      
                  }else if(lastDay < dayNumber){
                      weekData[i] = '';
                  }else{
                      weekData[i] = dayNumber;
                      dayNumber ++;
                  }
              }
              calendar.push(weekData); 
          }
          return calendar;
  })
    
  
    const lastMonth = () => {
          if(month.value == 1){
              year.value --;
              month.value = 12;
          }else{
              month.value --;
          }
      }
    const nextMonth = () => {
        if(month.value == 12){
            year.value ++;
            month.value = 1;
        }else{
            month.value ++;
        }
    }

    const isToday = (day) => {
        let date = year.value + "-" + month.value + "-" + day;
        if(today.value == date){
            return true;
        }
        return false;
    }
  
  
  
  onMounted(() => {
      let date = new Date();
      year.value = date.getFullYear();
      month.value = date.getMonth() + 1;
      let actualDay = date.getDate();
      today.value = year.value + '-' + month.value + '-' + actualDay;
  })
  
</script>

<template>
  <div>
      <div id="header">
          <span 
              class="header-arrow"
              style="cursor: pointer;"
              @click="lastMonth"
          >＜</span>
          <span>{{year}}年{{month}}月</span>
          <span 
              class="header-arrow"
              style="cursor: pointer;"
              @click="nextMonth"
          >＞</span>
      </div>
  </div>
  <div>
      <table id="main">
          <thead>
              <th 
                  v-for="(dayName,dayIndex) in weekdays"
                  :key="dayIndex"
              >{{dayName}}</th>
          </thead>
          <tbody>
              <tr
                  v-for="(weekData,weekDataIndex) in calendar"
                  :key="weekDataIndex"
              >
                  <td
                      v-for="(dayNumber,dayNumberIndex) in weekData"
                      :key="dayNumberIndex"
                      :class="{'today':isToday(dayNumber)}"                 
                  >
                      <span v-if="isToday(dayNumber)" id="todayStyle">today</span>            
                      <span v-else>{{dayNumber}}</span>                     
                  </td>
             </tr>
          </tbody>
      </table>
  </div>
  
  <div class="example-basic">
    <el-time-picker v-model="value1" placeholder="time" /><br>
</div>
<div class="button">
  <el-button type="primary">decisition</el-button>
  </div>
</template>



<style scoped>
  #main {
      font-size:14px;
      line-height:20px;
      table-layout: fixed;
      width: 100%;
      margin-bottom: 1rem;
      color: #212529;
      border-bottom: 1px solid #ddd;
      border-collapse: collapse;
  }
  #main th {
      padding: 0;
      text-align: center;
      vertical-align: middle;
      font-weight: bold;
      color: #999;
  }
  #main td {
      padding: 8px;
      text-align: center;
      vertical-align: middle;
      border-top: 1px solid #ddd;
  }
  .today {
      background-color: rgb(229, 236, 240);
  }
  #header {
      font-size: 24px;
      padding: 0;
      text-align: center;
      margin-bottom: 10px; 
      background-color: rgb(163, 229, 235);
      border-bottom: 1px solid #ddd;
      display:flex;
      justify-content: space-between;
  }
  #header span{
    font-weight: 900;
      padding:15px 20px;
      color: white;
      display: inline-block;
  }
  #todayStyle{
    border: solid;
    border-radius: 10px;
    color: white;
    font-weight: 600;
    background-color: rgb(58, 129, 229);
  }
  .example-basic  {
  margin: 20px ;
}
.button{
    margin-top: 20px;
}
</style>