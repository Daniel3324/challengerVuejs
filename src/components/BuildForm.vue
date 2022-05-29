<template>
  <div class="main">
    <h1>{{ msg }}</h1>
    <div class="form-main">
      <div class="form-send">
        <vue-form-generator :schema="schema"></vue-form-generator>
        <button @click="procesar()">Create Json</button>
      </div>
      <div class="form-build">
        <form action class="form" @submit.prevent="buildForm">        
          <label class="form-label " for="#type_input">Select type of field</label><br>          
          <select class="form-input" name="type_input" v-model="type_input" required>
            <option value="text">Text Input</option>
            <option value="date">Date Input</option>
            <option value="select">Select Input</option>
          </select>

          <label class="form-label" for="#label_input">Label</label><br>
          <input v-model="label_input" class="form-input" type="text" id="label_input" required><br>

          <label class="form-label" for="#name_input">Field Name</label><br>
          <input v-model="name_input" class="form-input" type="text" id="name_input" required><br>

          <label class="form-label" for="#option_input">Options (if the field is select) separet with [,]</label><br>
          <input v-model="option_input" class="form-input" type="text" id="option_input"><br>

          <input class="form-submit" type="submit" value="Create Input">
        </form>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'BuildForm',
  props: {
    msg: String
  },
  data: () => ({
    type_input: "",
    label_input: "",
    name_input: "",
    option_input: "",
    schema: "",
    campo: "",
    fields2:[],
    ids_input:[],
    fields: "",
    Json: ""
  }),
  methods: {
    buildForm() {
      
      if(this.type_input =="select"){

        this.campo = {
            type: 'select',
            id: this.name_input,
            label: this.label_input,
            required: true,
            values: ["The Terminator", "Judgment Day", "Rise of the Machines"]
        }
        this.fields2.push(this.campo);
      }else{   
        this.campo ={
            type: 'input',
            id: this.name_input,
            inputType: this.type_input,
            label: this.label_input,
            required: true
        }
        
        this.fields2.push(this.campo);    
      }        
      this.schema= {
          fields: this.fields2,
      }
      this.ids_input.push(this.name_input); 
       this.type_input="";
       this.label_input="";
       this.name_input="";
       this.option_input=""; 
    },
    
    procesar() { 
        var arrayToJson=[];
        this.ids_input.forEach(function(element) {        
            const MyObject = {element: document.getElementById(element).value};
            arrayToJson.push(MyObject); 
      });
      this.Json = JSON.stringify(arrayToJson);
      console.log(this.Json)
    }
  }
}
</script>

<style scoped>
.form-main {
  height: 800px;
  display: flex;
  gap: 30px;
}

.form-send {
  background-color: #e5efef;
  height: 100%;
  width: 60%;
}

.form-build {
  background-color: #e5efef;
  height: 100%;
  width: 40%;    
  display: flex;
  padding-top: 25px;
  text-align: left;  
}
.form{
  margin-left: 15px;
  width: 70%;
}
.form-input{
  height: 30px;
  background-color: #bbbbbb;
  width: 100%;
  margin-top: 0px;
  margin-bottom: 30px;
}
.form-control{
  height: 30px;
  background-color: #bbbbbb;
  width: 100%;
  margin-top: 0px;
  margin-bottom: 30px;
}
</style>