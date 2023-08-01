<template>
  <body>
    <main>
      <div class="mainDiv">
        <h1 class="heading">VUE JS <br /></h1>
        <br />
        <h2>1. Two way data binding</h2>

        <div>
          <h3 class="heading">Full Name</h3>
          <input type="text" placeholder="enter full name" v-model="name" class="name" />
          <label>{{ this.name }}</label>

          <h3 class="heading">Fathers Name</h3>
          <input type="text" placeholder="enter fathers name" v-model="fathername" class="name" />

          <h3 class="heading">Email</h3>
          <input type="email" placeholder="enter your email" v-model="email" class="name" />

          <h3 class="heading">password</h3>
          <input
            type="password"
            placeholder="enter your password"
            v-model="password"
            class="name"
          /><br />
          <br />
          <button class="login" v-on:click="login" type="button">LOGIN</button><br /><br />
        </div>
        <hr /><br>
        <h2 class="heading">2. Conditional Rendering<br /></h2>
        <h3 class="heading">v-if</h3>
        <label v-if="flag">this is text 1</label>
        <button @click="showText">Show Text</button>
        <button @click="hideText">Hide Text</button>
        <h3 class="heading">v else</h3>
        <label v-if="xxx">xxx is shown</label>
        <label v-else>cannot show</label><br />
        <button id="text" @click="alphabets">Hide Text</button>
        <h3 class="heading">else if <br /></h3>
        <label v-if="fruits == 'orange'">fruits are shown</label>
        <label v-else-if="fruits == 'banana'"> </label>
        <label v-else>empty space</label><br /><br>
        <hr />
        <div><br>
          <h2 class="heading">3. Event Handling<br /></h2>
          <h3>Button</h3>
          <button v-on:click="color = 'orange'">change color</button><br />
          <label>{{ color }}</label>
          <h3>Input Field</h3>
          <input placeholder="enter value" v-model="value" @blur="saveValue(this.value)" /><br />
          <h3>Dropdown</h3>
          <div>
            <label for="cars">Choose a car:</label>

            <select
              v-model="selectedValue"
              id="car"
              name="cars"
              @change="saveCars(this.selectedValue)"
            >
              <option v-for="item in cars" :key="item">{{ item.type }}</option>
            </select>
            <div>
              <h3>Radio Button</h3>

              <input
                @change="RadioBtnOnChange(this.radioCheck)"
                type="radio"
                id="yes"
                name="yes"
                value="yes"
                v-model="radioCheck"
              />
              <label for="yes">Yes</label><br />
              <input
                @change="RadioBtnOnChange(this.radioCheck)"
                type="radio"
                id="no"
                name="no"
                value="no"
                v-model="radioCheck"
              />
              <label for="no">No</label><br />
              <p>Selected: {{ radioCheck }}</p>

              <h3>Checkbox</h3>
              <input
                @change="CheckBoxOnChange(this.subscribe)"
                type="checkbox"
                id="subscribe"
                value="subscribe"
                name="subscribe"
                v-model="subscribe"
              />
              <label for="apple">Subscribe</label><br />

              <p>Subscribed: {{ subscribe }}</p>
            </div><br>
            <hr />
            <div><br>
              <h2 class="heading">4. List Rendering<br /></h2>
              <ul>
                <li v-for="value in numbers" :key="value">
                  {{ value }}
                </li>
              </ul>
            </div>
            <hr /><br>
            <div>
              <h2 class="heading">5. Watchers<br /></h2>
              <h3>Sum of two numbers</h3>
              Enter number 1:<input type="number" name="number1" v-model="number1" />
              <p></p>
              Enter number 2:<input type="number" name="number2" v-model="number2" />
              <p></p>
              <button @click="add()">Sum</button>
              <hr />
              <p>TOTAL:{{ result }}</p>
            </div>
            <h3>Increment</h3>
            <button v-on:click="counter++">Increment</button>
            <p>INCREMENT: {{ counter }}</p>
          </div><hr><br>
          <div>
            <h2 class="heading">6. Vue template refs<br /></h2>
            <p>Click the button to say Hello.</p>
            <button @click="changeVal">Change Text</button>
            <p ref="ref1">This is the initial text</p>
          </div><hr><br>
          <div>
            <h2 class="heading">6. Emit <br /></h2>


          </div>
          <GenericTextBox :codeValue ="selectCode" :ButtonLabel="ButtonValue" />
          
        </div>
      </div>
    </main>
  </body>
</template>
<script>
import { reactive, ref } from 'vue'
import GenericTextBox from '../components/GenericTextBox.vue';

export default {
  components:{
    GenericTextBox
  },
  data() {
    return reactive({
      selectCode: 'javascript',
      ButtonValue: 'hello',

      name: '',
      fathername: '',
      email: '',
      password: '',
      flag: false,
      xxx: true,
      fruits: 'yellow',
      color: ref('blue'),
      value: '',
      selectedValue: 'KIA',
      childVal:"hello child",
      childLabel:"Name from Parent",
      cars: [
        {
          type: 'KIA'
        },
        {
          type: 'KIA1'
        },
        {
          type: 'KIA-X'
        },
        {
          type: 'KIA3'
        },
        {
          type: 'ALTO'
        }
      ],
      radioCheck: '',
      subscribe: null,
      numbers: [10, 20, 90, 200, 100],
      // num1: null,
      // num2: null,
      // sum: computed(() => parseInt(state.num1) + parseInt(state.num2)),
      number1: 0,
      number2: 0,
      result: 0,
      counter: 0
    })
  },
  methods: {
    parentSaveValue(val){
      alert("value of child is this => "+val)
    },
      changeVal() {
        this.$refs.ref1.innerHTML = "Hello!";
        this.$refs.ref1.style.color = "red";

      },
    increment() {
      this.counter++
    },

    add() {
      this.result = parseInt(this.number1) + parseInt(this.number2)
    },

    sort(numbers) {
      return [...numbers].sort((a, b) => a - b)
    },

    RadioBtnOnChange(val) {
      alert("Radio Btn's value is now " + val)
    },
    CheckBoxOnChange(val) {
      alert('subscrive value is now ' + val)
    },
    saveCars(val) {
      console.log('you can use this value fo multiple purpose late on', val)
    },
    login() {
      console.warn(this.from)
    },
    showText() {
      this.flag = true
    },
    hideText() {
      this.flag = false
    },
    alphabets() {
      if (this.xxx) {
        this.xxx = false
        document.getElementById('text').innerHTML = 'Show Text'
      } else {
        this.xxx = true
        document.getElementById('text').innerHTML = 'Hide Text'
      }
    },
    saveValue(val) {
      alert(val)
      this.value = val
    }
    /* fruits(){
      if(this.fruits){
        this.fruits = false
      }else if(this.fruits){
        this
      } */
  },
  computed: {
    result() {
      return parseInt(this.number1) + parseInt(this.number2)
    }
  },
  mounted() {
    // alert('hello from mounted')
  },
  watch: {
    subscribe(newVal, OldVal) {
      console.log('newVal => ' + newVal, 'old value => ' + OldVal)
    },
    counter(NewVal, OldVal) {
      console.log('NewVal =>' + + NewVal, 'old value => ' + OldVal)
      this.counter = NewVal + OldVal
      
    }

  }
}
</script>
<style scoped>
input {
  padding: 10px 50px;
  margin: 4px;

  text-align: left;
}

span {
  font-size: 18px;
  margin: 4px;
  font-weight: 500;
  vertical-align: top;
  text-align: left;
}
.name {
  font-family: 'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif;
  font-size: small;

  text-align: left;
}
.login {
  font-size: medium;
  text-align: center;
}
.mainDiv {
  color: hsla(160, 100%, 37%, 1);
  transition: 10s;
}
button {
  display: inline-block;
  background-color: #7b38d8;
  padding: 10px;
  width: 120px;
  color: #ffffff;
  text-align: center;
}
h2 {
  text-decoration: underline;
}
#car {
  padding: 5px;
  margin-left: 20px;
  width: 150px;
}
</style>
