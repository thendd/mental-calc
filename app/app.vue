<template>
  <UHeader title="Mental math" />
  <UMain>
    <h2>
      {{ currentOperation?.left }} {{ currentOperation?.sign }}
      {{ currentOperation?.right }} = x
    </h2>
    <input v-model="givenAnswer" :oninput="onChange" />
  </UMain>
</template>

<script setup lang="ts">
type Operation = {
  left: number
  right: number
  sign: string
  answer: number
  worth: number
}

let grade = 1

const generateRandomNumber = (min: number, max: number) => {
  min = Math.ceil(min)
  max = Math.floor(max)
  return Math.floor(Math.random() * (max - min + 1)) + min
}

const newOperation = () => {
  const operationSigns = ['+', '-', 'x', '/']
  let left = 0
  let right = 0
  let answer = 0
  let worth = 0
  let operationSign = '+'

  if (grade < 1.5) {
    left = generateRandomNumber(0, 10)
    right = generateRandomNumber(0, 10)

    operationSign = operationSigns[generateRandomNumber(0, 1)] as string
    worth = 0.1
  }

  switch (operationSign) {
    case '+':
      answer = left + right
      break
    case '-':
      answer = left - right
      break
    case 'x':
      answer = left * right
      break
    case '/':
      answer = left / right
  }

  return {
    left,
    right,
    answer,
    worth,
    sign: operationSign,
  }
}

const currentOperation = ref<Operation>()

const givenAnswer = ref<number | undefined>()

const onChange = (event: InputEvent) => {
  const { value } = event.target as HTMLInputElement
  console.log(Number(value), currentOperation.value?.answer)
  if (Number(value) === currentOperation.value?.answer) {
    grade += currentOperation.value.worth
    currentOperation.value = newOperation()
    givenAnswer.value = undefined
  }
}

onMounted(() => {
  currentOperation.value = newOperation()
})
</script>
