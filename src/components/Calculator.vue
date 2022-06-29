<template>
  <div class="calculator">
    <div class="container-fluid">
      <div class="row justify-content-center align-items-center">
        <subject v-bind:isHeader=true ></subject>
        <div v-for="(item,index) in subjects" style="padding:0;" :key="index">
          <subject :index="index" :name="item.name" :cred="item.cred" :grade="item.grade" v-bind:isInput="false" @update="removeSubject"></subject>
        </div>
        <subject v-bind:isInput="true" @update="addSubject"></subject>
      </div>
    </div>

    <div class="container-fluid">
      <div class="row justify-content-center align-items-center">
        <h4 class="col-4">
          <span>GPA {{sumGpa}}</span>
        </h4>
        <h4 class="col-4">
          <span>總學分 {{sumCred}}</span>
        </h4>
      </div>
    </div>
  </div>
</template>

<script>
import Subject from './Subject.vue'
export default {
  name: 'Caculator',
  components: {
    Subject
  },
  props: {
  },
  data() {
    return {
      gpa : 0 ,
      subjects : []
    }
  },
  methods : {
    gradeVal(grade) {
      if(grade == "A+") return 4.3;
      if(grade == "A") return 4.0;
      if(grade == "A-") return 3.7;
      if(grade == "B+") return 3.3;
      if(grade == "B") return 3.0;
      if(grade == "B-") return 2.7;
      if(grade == "C+") return 2.3;
      if(grade == "C") return 2.0;
      if(grade == "C-") return 1.7;
      if(grade == "D") return 1.0;
      if(grade == "E") return 0;
      if(grade == "X") return 0;
      return 0;
    },
    addSubject(name,cred,grade) {
      this.subjects.push({
        name : name == "" ? "未命名" : name,
        cred : cred,
        grade : grade,
      });
      return true;
    },
    removeSubject(index) {
      this.subjects.splice(index,1);
    }
  },
  mounted () {
  },
  computed : {
    sumGpa : function() {
      if(this.subjects.length == 0) return 0;
      let result = this.subjects.reduce((acc, cur) => {
        return acc + cur.cred * this.gradeVal(cur.grade);
      }, 0) / this.subjects.reduce((acc, cur) => { return acc + cur.cred; }, 0);
      return result.toFixed(3);
    },
    sumCred : function() {
      return this.subjects.reduce((acc, cur) => {
        return acc + cur.cred;
      }, 0);
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}

.collist {
  display : flex;
  flex-flow : column nowrap;
  justify-content: center;
  align-items: center;
  align-content: center;
}

.collist * { 
  margin: 3px;
}
.rowlist * { 
  margin: 3px;
}

.rowlist {
  display : flex;
  flex-flow : row nowrap;
  justify-content: center;
  align-items: center;
  align-content: center;
}

.container-fluid {
  padding: auto;
}

</style>
