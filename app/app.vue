<template>
  <UHeader title="Mental math" />
  <UMain>
    <h2>
      {{ currentOperation.left }} {{ currentOperation.sign }}
      {{ currentOperation.right }} = x
    </h2>
    <UForm @submit.prevent="onSubmit">
      <UFormField>
        <UInput
          v-model="givenAnswer"
          type="number"
        />
      </UFormField>
      <UButton
        type="submit"
        label="Guess"
      />
    </UForm>
  </UMain>
</template>

<script setup lang="ts">
type Operation = {
  left: number
  right: number
  sign: string
  answer: number
}

const currentOperation: Operation = {
  left: 3,
  right: 2,
  sign: '+',
  answer: 3 + 2,
}

const givenAnswer = ref<number>()

const isGivenAnswerCorrect = () => {
  return givenAnswer.value == currentOperation.answer
}

const onSubmit = () => {
  alert(isGivenAnswerCorrect() ? 'correct' : 'wrong loser')
}
</script>
