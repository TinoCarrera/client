<template>
  <form @submit.prevent="createFAQ">
    <div class="field">
      <label class="label">Question</label>
      <div class="control">
        <input
          v-model="question"
          class="input"
          type="text"
          name="question"
          placeholder="e.g How?"
          required
        />
      </div>
    </div>

    <div class="field">
      <label class="label">Answer</label>
      <div class="control">
        <textarea
          v-model="answer"
          class="textarea"
          name="answer"
          rows="5"
          placeholder="e.g. Because."
        />
      </div>
    </div>

    <button type="submit" class="button is-success">Create</button>
  </form>
</template>

<script>
import { ref } from "vue";
import { useRouter } from "vue-router";

export default {
  setup() {
    const { router } = useRouter();
    const question = ref("");
    const answer = ref("");

    const API_URL = "http://localhost:5000/api/v1/faqs";

    async function createFAQ() {
      const response = await fetch(API_URL, {
        method: "POST",
        headers: {
          "content-type": "application/json",
        },
        body: JSON.stringify({
          question: question.value,
          answer: answer.value,
        }),
      });
      const json = await response.json();
      console.log(json);
      if (response.ok) {
        // redirect!
        router.push({
          name: "Home",
        });
      } else {
        // show an error!
      }
    }

    return {
      question,
      answer,
      createFAQ,
    };
  },
};
</script>

<style>
</style>