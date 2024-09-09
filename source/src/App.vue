<template>
  <div class="app" :class="{themeApex:changeTheme}">

    <div class="card">
      <div class="card_side card_side--front" :class="{vueRotateFront:rotationOn}">
        <div class="form-row">
          <label for>ID</label>
          <br />
          <input disabled type="text" v-model="employee_id" />
        </div>
        <div class="form-row">
          <label for>FIRST NAME</label>
          <br />
          <input type="text" v-model="first_name" />
        </div>
        <div class="form-row">
          <label for>LAST NAME</label>
          <br />
          <input type="text" v-model="last_name" />
        </div>
        <div class="form-row">
          <label for>EMAIL</label>
          <br />
          <input type="text" v-model="email" />
        </div>
        <div class="form-row">
          <label for>PHONE NUMBER</label>
          <br />
          <input type="text" v-model="phone_number" />
        </div>
        <div class="form-row">
          <label for>HIRE DATE</label>
          <br />
          <input disabled type="text" v-model="hire_date" />
        </div>
        <div class="form-row">
          <label for>JOB ID</label>
          <br />
          <input disabled type="text" v-model="job_id" />
        </div>
        <div class="form-row">
          <label for>SALARY</label>
          <br />
          <input type="text" v-model="salary" />
        </div>
        <div @click="submitValues" class="dugme">
          <span>Submit to</span>
          <br />
          <span>Database</span>
        </div>
      </div>
      <div
        class="card_side card_side--back card_side--back-1"
        :class="{vueRotateBack:rotationOn,themeApex:changeTheme}">
        <img
          class="vueLogo"
          src="https://cdn.iconscout.com/icon/free/png-256/vuejs-1175052.png"
          alt
        />
      </div>
    </div>
  </div>
</template>

<script>




export default {
  name: "app",
  data() {
    return {
      employee_id: null,
      first_name: null,
      last_name: null,
      email: null,
      phone_number: null,
      hire_date: null,
      job_id: null,
      salary: null,
      changeTheme: false,
      rotationOn: false
    };
  },
  methods: {
    apexFunction() {
      this.employee_id = window.apex.item("P2_EMPLOYEE_ID").getValue();
      this.first_name = window.apex.item("P2_FIRST_NAME").getValue();
      this.last_name = window.apex.item("P2_LAST_NAME").getValue();
      this.email = window.apex.item("P2_EMAIL").getValue();
      this.phone_number = window.apex.item("P2_PHONE_NUMBER").getValue();
      this.hire_date = window.apex.item("P2_HIRE_DATE").getValue();
      this.job_id = window.apex.item("P2_JOB_ID").getValue();
      this.salary = window.apex.item("P2_SALARY").getValue();
    },
    submitValues() {
      if (this.employee_id) {
        window.apex.item("P2_FIRST_NAME").setValue(this.first_name);
        window.apex.item("P2_LAST_NAME").setValue(this.last_name);
        window.apex.item("P2_EMAIL").setValue(this.email);
        window.apex.item("P2_PHONE_NUMBER").setValue(this.phone_number);
        window.apex.item("P2_HIRE_DATE").setValue(this.hire_date);
        window.apex.item("P2_JOB_ID").setValue(this.job_id);
        window.apex.item("P2_SALARY").setValue(this.salary);
        window.apex.item("P2_FIRE").setValue();
        this.rotationOn = true;
        setTimeout(() => {
          this.employee_id = null;
          this.first_name = null;
          this.last_name = null;
          this.email = null;
          this.phone_number = null;
          this.hire_date = null;
          this.job_id = null;
          this.salary = null;
        }, 300);
        setTimeout(() => {
          this.rotationOn = false;
        }, 2500);
      }
    }
  },
  mounted() {
    var self=this;
    window.onload = () => {
          document.getElementById("changeTheme").onclick = () => {
            this.changeTheme = !this.changeTheme;
          };   
          const targetNode = document.getElementById('P2_FIRST_NAME');
          const config = { attributes: true, childList: true, subtree: true };
          const callback = function(mutationsList, observer) {
            for(let mutation of mutationsList) {
              // console.log(mutation);
              if (mutation.target.value != '') {
                    console.log('The Region was modified. Item '+mutation.attributeName+' was changed. Its '+ mutation.target.value+' now');
                    self.apexFunction();
              }
            }
          };
          const observer = new MutationObserver(callback);
          observer.observe(targetNode, config);
    };
  }
}
</script>

<style lang="scss">
.app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  background: rgb(66, 184, 131);
  background: linear-gradient(
    153deg,
    rgba(66, 184, 131, 1) 0%,
    rgba(53, 73, 94, 1) 40%,
    rgba(53, 73, 94, 1) 60%,
    rgba(66, 184, 131, 1) 100%
  );
  color: #2c3e50;
  padding: 50px 0;
}
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.form {
  padding: 10px;
  border: 1px solid white;
  border-radius: 10px;
  width: 60%;
  height: 90%;
  margin: 10px auto;
  background-color: rgba(255, 255, 255, 0.3);
  width: 50%;
  margin: 0 auto;
  display: flex;
  flex-wrap: wrap;
  position: relative;

  &-row {
    padding: 6px 0;
    flex: 0 0 100%;
    text-align: center;
  }
}
input {
  border: none;
  border-radius: 5px;
  outline-color: #42b883;
  padding: 5px 10px;
  margin: 5px;
  -webkit-box-shadow: 0px 0px 10px 0px #35495e;
  -moz-box-shadow: 0px 0px 10px 0px #35495e;
  box-shadow: 0px 0px 10px 0px #35495e;
}
label {
  margin: 5px;
  color: white;
  font-size: 17px;
}
.dugme {
  cursor: pointer;
  border: 2px solid white;
  border-radius: 10px;
  margin: 0 auto;
  margin-top: 20px;
  padding: 10px;
  font-size: 20px;
  color: white;
  font-weight: 700;
  background-color: #35495e94;
  &:hover {
    -webkit-box-shadow: 0 10px 10px -5px #35495e;
    -moz-box-shadow: 0 10px 10px -5px #35495e;
    box-shadow: 0 10px 10px -5px #35495e;
    transform: translateY(-2px);
  }
}
.themeApex {
  background: linear-gradient(
    153deg,
    rgba(0, 118, 223, 1) 0%,
    rgba(51, 61, 70, 1) 45%,
    rgba(51, 61, 70, 1) 60%,
    rgba(0, 118, 223, 1) 100%
  ) !important;
}

.card {
  //Functionality
  perspective: 150rem;
  -moz-perspective: 150rem;
  position: relative;
  width: 50%;
  margin: 0 auto;

  &_side {
    font-size: 2rem;
    transition: all 0.8s ease;
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    backface-visibility: hidden;
    border-radius: 3px;
    overflow: hidden;
    box-shadow: 0 1.5rem 4rem rgba(black, 0.15);

    &--front {
      padding: 10px;
      border: 1px solid white;
      border-radius: 10px;
      width: 100%;
      height: 100%;
      margin: 10px auto;
      background-color: rgba(255, 255, 255, 0.3);
      margin: 0 auto;
      display: flex;
      flex-wrap: wrap;
      position: relative;

      &-row {
        padding: 6px 0;
        flex: 0 0 100%;
        text-align: center;
      }
    }
    &--back {
      height: 100%;
      border: 1px solid white;
      border-radius: 10px;
      transform: rotateY(180deg);
      &-1 {
        background: linear-gradient(
          153deg,
          rgba(66, 184, 131, 1) 0%,
          rgba(53, 73, 94, 1) 40%,
          rgba(53, 73, 94, 1) 60%,
          rgba(66, 184, 131, 1) 100%
        );
      }
    }
  }
}
.vueLogo {
  height: 30%;
  display: block;
  margin: 45% auto;
}
.vueRotateFront {
  animation: rotation 2s linear;
}
.vueRotateBack {
  animation: rotationInvert 2s linear;
}
@keyframes rotation {
  0% {
    transform: rotateY(-360deg);
  }
  50% {
    transform: rotateY(-180deg);
  }
  100% {
    transform: rotateY(0);
  }
}
@keyframes rotationInvert {
  0% {
    transform: rotateY(-180deg);
  }
  50% {
    transform: rotateY(0);
  }
  100% {
    transform: rotateY(180deg);
  }
}
</style>
