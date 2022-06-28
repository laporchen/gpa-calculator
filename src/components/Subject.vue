<template>
  <div class="subject">
    <div class="container-fluid bg">
      <div class="row justify-content-center align-items-center">
        <template v-if="isHeader">
          <div class="col-lg-3 col-6 col-sm-4"><strong>科目</strong></div>
          <div class="col-lg-1 col-2 col-sm-2"><strong>成績</strong></div>
          <div class="col-lg-1 col-2 col-sm-2"><strong>學分</strong></div>
        </template>
        <template v-else-if="isInput === false">
            <div class="col-lg-3 col-6 col-sm-4">
              {{name}}
            </div>
            <div class="col-lg-1 col-2 col-sm-2">
              {{grade}}
            </div>
            <div class="col-lg-1 col-2 col-sm-2 ">
              {{cred}}
            </div>
        </template>
        <template v-else>
              <div class="col-lg-3 col-6 col-sm-4 ">
                <input type="text" v-model="inputName" placeholder="名稱">
              </div>
              <div class="col-lg-1 col-2 col-sm-2 ">
                <select v-model="inputGrade">
                  <option >A+</option>
                  <option >A</option>
                  <option >A-</option>
                  <option >B+</option>
                  <option >B</option>
                  <option >B-</option>
                  <option >C+</option>
                  <option >C</option>
                  <option >C-</option>
                  <option >E</option>
                  <option >X</option>
                </select>
              </div>
              <div class="col-lg-1 col-2 col-sm-2 ">
                <input type="number" @keypress="isNumber($event)" v-model="inputCred" min=1 placeholder="">
              </div>
        </template>
        <div class="col-lg-1 col-2 col-sm-3">
          <button class="btn btn-danger btn-sm" @click="remove" v-if="isInput !== true && isHeader == false" >刪除</button>
          <button class="btn btn-primary btn-sm" @click="add" v-if="isInput == true && isHeader == false" >新增</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Subject',
  props: {
    name : String,
    grade : String,
    cred : Number,
    isInput : Boolean,
    isHeader : Boolean,
    index : Number,
  },
  data () {
    return {
      inputName : "",
      inputGrade : 0,
      inputCred : "",
    }
  },
  methods : {
    isNumber(evt) {
      evt = (evt) ? evt : window.event;
      var charCode = (evt.which) ? evt.which : evt.keyCode;
      if (charCode > 31 && (charCode < 48 || charCode > 57)) {
        evt.preventDefault();
      } else {
        return true;
      }
    },
    remove () {
      this.$emit('update',this.index);
    },
    add () {
      if(isNaN(this.inputCred) || this.inputGrade == "") {
        alert("Please fill all the fields");
        return;
      }
      else if(this.inputCred <= 0) {
        alert("Credit invalid.");
        return;
      }
      this.$emit('update',this.inputName,parseInt(this.inputCred),this.inputGrade)
      this.inputName = "";
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

div {
  height: auto;
}
.col-lg-1, .col-lg-3  {
  height: auto;
}

.col-sm-4, .col-sm-2, .col-sm-3 {
  height:auto;
}
.col-6, .col-2 {
  height: auto;
}
.bg {
  border-right: 1px dotted #fff;
  background:#f0f0f0;
}
.col-6 input {
  width: 90%;
  max-width: 100%;
}
.col-2 input {
  width: 100%;
  
}
.col-lg-4 input {
  width: 80%;
}
div { 
  padding-top: 2px;
  padding-bottom: 2px;
  vertical-align: middle;
}
</style>
