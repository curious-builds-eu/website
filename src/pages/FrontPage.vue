<template>
  <q-page class="container">
    <section class="hero">
      <div>
        <h1>Curious Builds</h1>
        <p class="subtitle">Information technology consulting</p>
      </div>
    </section>

    <q-card flat>
      <q-card-section>
        <h4>Software Automation Solutions</h4>
        <p>
          Our company has been supplying automation solutions for software development
          teams since 2015. We help develop innovative solutions for building software
          that help teams improve their productivity and efficiency.
        </p>
      </q-card-section>
      <q-separator inset />
      <q-card-section>
        <h4>Agricultural IoT Solutions</h4>
        <p>
          The company has developed its own IoT devices for small scale farms and
          homesteads, focusing on automating irrigation and task management around the
          entire lifecycle of crops.
        </p>
      </q-card-section>
    </q-card>
  </q-page>
</template>
<script setup lang="ts">
import { ref } from "vue";

const email = ref("");
const submitting = ref(false);
const success = ref(false);
const error = ref(false);

async function onSubmit() {
  error.value = false;
  success.value = false;
  if (!email.value || !/.+@.+\..+/.test(email.value)) return;
  submitting.value = true;
  try {
    const endpoint =
      (window as any).SUBSCRIBE_ENDPOINT || "https://formspree.io/f/xwpqapdd";
    const res = await fetch(endpoint, {
      method: "POST",
      headers: { "Content-Type": "application/json", Accept: "application/json" },
      body: JSON.stringify({ email: email.value }),
    });
    if (res.ok) {
      success.value = true;
      (window as any).umami?.track?.("notify-me");
      email.value = "";
    } else error.value = true;
  } catch (e) {
    error.value = true;
  } finally {
    submitting.value = false;
  }
}
</script>

<style scoped>
h4 {
  margin-top: 0.5rem;
  margin-bottom: 0.4rem;
}

.form-message {
  margin-top: 6px;
  font-size: 0.9rem;
}
</style>
