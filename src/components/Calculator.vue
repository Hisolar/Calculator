<template>
  <section class="bg-yellow-500 min-h-screen flex items-center justify-center">
    <article class="bg-red-600 w-[400px] h-[500px]">
      <div class="container mx-auto px-8">
        <div class="bg-red-100 w-full h-20 mt-8 text-2xl px-4 py-2">
          <div>{{ first_value }} {{ operand }} {{ second_value }}</div>
        </div>
        <main class="grid gap-4 mt-4">
          <div v-for="(button_group, index) in calculatorButtons" :key="index">
            <div class="grid grid-cols-4 items-center gap-4">
              <button
                @click="handleButtonClick(button)"
                v-for="button in button_group"
                :key="button.value"
                class="bg-black text-white p-4"
                :class="[
                  button.value == '0' ? 'col-span-2' : '',
                  button.value == 'equal' ? 'col-span-3' : '',
                ]"
              >
                {{ button.name }}
              </button>
            </div>
          </div>
        </main>
      </div>
    </article>
  </section>
</template>
<script setup>
import { ref } from "vue";

const calculatorButtons = [
  [
    {
      value: "*",
      name: "X",
      type: "operand",
    },

    {
      value: "+",
      name: "+",
      type: "operand",
    },

    {
      value: "-",
      name: "-",
      type: "operand",
    },

    {
      value: "/",
      name: "/",
      type: "operand",
    },
  ],
  [
    {
      value: 0,
      name: "0",
      type: "numbers",
    },
    {
      value: 1,
      name: "1",
      type: "numbers",
    },

    {
      value: 2,
      name: "2",
      type: "numbers",
    },

    {
      value: 3,
      name: "3",
      type: "numbers",
    },

    {
      value: 4,
      name: "4",
      type: "numbers",
    },

    {
      value: 5,
      name: "5",
      type: "numbers",
    },

    {
      value: 6,
      name: "6",
      type: "numbers",
    },

    {
      value: 7,
      name: "7",
      type: "numbers",
    },

    {
      value: 8,
      name: "8",
      type: "numbers",
    },

    {
      value: 9,
      name: "9",
      type: "numbers",
    },

    {
      value: ".",
      name: ".",
      type: "numbers",
    },
  ],

  [
    {
      value: "all_clear",
      name: "AC",
      type: "function",
    },

    {
      value: "equal",
      name: "=",
      type: "function",
    },
  ],
];

const first_value = ref("");
const second_value = ref("");
const operand = ref("");
const function_key = ref("");

const handleButtonClick = (button) => {
  if (button.type == "numbers" && operand.value.length == 0) {
    first_value.value = first_value.value + button.value;
  } else if (button.type == "numbers" && operand.value.length != 0) {
    second_value.value = second_value.value + button.value;
  } else if (button.type == "operand") {
    operand.value = button.value;
  } else if (button.type == "function" && button.value == "all_clear") {
    first_value.value = "";
    second_value.value = "";
    operand.value = "";
  } else if (button.type == "function" && button.value == "equal") {
    switch (operand.value) {
      case "+":
        first_value.value =
          Number(first_value.value) + Number(second_value.value);
        break;

      case "-":
        first_value.value =
          Number(first_value.value) - Number(second_value.value);
        break;

      case "*":
        first_value.value =
          Number(first_value.value) * Number(second_value.value);
        break;

      case "/":
        first_value.value =
          Number(first_value.value) / Number(second_value.value);
        break;

      default:
        console.log("Error `occured");
        break;
    }

    second_value.value = "";
    operand.value = "";
  }
};
</script>
