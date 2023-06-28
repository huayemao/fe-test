<script setup lang="tsx">
import { ButtonHTMLAttributes } from "nuxt/dist/app/compat/vue-demi";

const props = withDefaults(
  defineProps<{
    class: string;
    type: ButtonHTMLAttributes["type"];
  }>(),
  {
    type: "button",
  }
);
</script>

<template>
  <button
    :type="props.type"
    :class="[
      'rounded-xl bg-indigo-500 dark:bg-indigo-500 hover:enabled:bg-indigo-400 dark:hover:enabled:bg-indigo-400 text-white hover:enabled:shadow-lg hover:enabled:shadow-indigo-500/50 dark:hover:enabled:shadow-indigo-800/20 focus-visible:outline-indigo-400/70 focus-within:outline-indigo-400/70 focus-visible:bg-indigo-500 active:enabled:bg-indigo-500 dark:focus-visible:outline-indigo-400 dark:focus-within:outline-indigo-400 dark:focus-visible:bg-indigo-500 dark:active:enabled:bg-indigo-500 w-full',
      props.class,
    ]"
  >
    <span><slot /></span>
  </button>
</template>
