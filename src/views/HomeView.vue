<script setup>
import { ref } from 'vue'
import request from "../utils/requests"

const inputText = ref('')
const summary = ref('')

function summarize() {
  if (inputText.value.trim().length === 0) {
    summary.value = 'Please enter the text to summarize.'
    return
  }
  else{
    //Send request to backend
    let res = request.post("/summarize", { "message":inputText.value })
    res.then((result) => {
      summary.value = result.msg
    })
  }
  
}
</script>

<template>
  <div class="container">
    <h1>Text Summarizer</h1>
    <textarea
      v-model="inputText"
      placeholder="Enter the text to summarize"
      rows="8"
      class="input-area"
    ></textarea>
    <button class="summarize-btn" @click="summarize">Summarize</button>
    <div v-if="summary" class="summary-box">
      <h2>Summary Result</h2>
      <p>{{ summary }}</p>
    </div>
  </div>
</template>

<style scoped>
.container {
  max-width: 600px;
  width: 90vw;
  margin: 5vh auto;
  padding: 5vw 4vw;
  background: #fff;
  border-radius: 16px;
  box-shadow: 0 4px 24px rgba(0,0,0,0.08);
  display: flex;
  flex-direction: column;
  align-items: center;
}
h1 {
  margin-bottom: 24px;
  color: #2c3e50;
  font-size: 2rem;
  font-weight: bold;
  letter-spacing: 2px;
  text-align: center;
}
.input-area {
  width: 100%;
  min-height: 120px;
  padding: 16px;
  border: 1.5px solid #d0d7de;
  border-radius: 8px;
  font-size: 1rem;
  margin-bottom: 20px;
  resize: vertical;
  transition: border 0.2s;
  box-sizing: border-box;
}
.input-area:focus {
  border-color: #42b983;
  outline: none;
}
.summarize-btn {
  background: linear-gradient(90deg, #42b983 0%, #38a169 100%);
  color: #fff;
  border: none;
  border-radius: 8px;
  padding: 12px 32px;
  font-size: 1.1rem;
  cursor: pointer;
  margin-bottom: 24px;
  transition: background 0.2s;
  width: 100%;
  max-width: 200px;
}
.summarize-btn:hover {
  background: linear-gradient(90deg, #38a169 0%, #42b983 100%);
}
.summary-box {
  width: 100%;
  background: #f6f8fa;
  border-radius: 8px;
  padding: 18px 16px;
  margin-top: 8px;
  box-sizing: border-box;
  word-break: break-all;
}
.summary-box h2 {
  margin: 0 0 8px 0;
  font-size: 1.1rem;
  color: #25603c;
}
.summary-box p {
  margin: 0;
  color: #333;
  font-size: 1rem;
}
@media (max-width: 600px) {
  .container {
    padding: 6vw 2vw;
    max-width: 98vw;
  }
  .input-area {
    font-size: 0.95rem;
    min-height: 80px;
  }
  .summarize-btn {
    font-size: 1rem;
    padding: 10px 0;
  }
}
</style>
