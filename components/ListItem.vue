<script setup lang="tsx">
const props = defineProps<{
  title: string;
  initial: string;
  description: string;
}>();
</script>

<template>
  <div
    class="hover:bg-slate-100 focus-within:bg-slate-100 dark:hover:bg-slate-700/70 dark:focus-within:bg-slate-700/70 group flex items-center gap-3 p-2 rounded-xl"
  >
    <div
      class="relative inline-flex shrink-0 items-center justify-center outline-none h-8 w-8 rounded-full bg-indigo-100 dark:bg-indigo-500/20 text-indigo-500 ms-1 shrink-0"
    >
      <div
        class="flex h-full w-full items-center justify-center overflow-hidden text-center transition-all duration-300 rounded-full"
      >
        <span class="font-heading text-center font-medium uppercase text-sm">{{
          props.initial
        }}</span>
      </div>
    </div>
    <div>
      <h4
        class="font-heading text-xs font-light leading-tight text-slate-800 dark:text-white"
      >
        <span>{{ props.title }} </span>
      </h4>
      <p class="font-alt text-xs font-normal leading-normal leading-normal">
        <span class="text-slate-400">{{ props.description }}</span>
      </p>
    </div>
    <div
      class="ms-auto flex -translate-x-1 items-center opacity-0 transition-all duration-300 group-hover:translate-x-0 group-focus-within:translate-x-0 group-hover:opacity-100 group-focus-within:opacity-100"
    >
      <a
        aria-current="page"
        href="/#"
        class="router-link-active router-link-exact-active disabled:opacity-60 disabled:cursor-not-allowed hover:shadow-none false false text-slate-700 bg-white border border-slate-300 dark:text-white dark:bg-slate-700 dark:hover:bg-slate-600 dark:border-slate-600 hover:bg-slate-50 rounded-xl h-10 w-10 p-2 nui-focus relative inline-flex items-center justify-center space-x-1 font-sans text-sm font-normal leading-5 no-underline outline-none transition-all duration-300 scale-75"
        slate=""
        ><svg
          xmlns="http://www.w3.org/2000/svg"
          xmlns:xlink="http://www.w3.org/1999/xlink"
          role="img"
          class="icon h-4 w-4"
          width="1em"
          height="1em"
          viewBox="0 0 24 24"
        >
          <path
            fill="none"
            stroke="currentColor"
            stroke-linecap="round"
            stroke-linejoin="round"
            stroke-width="2"
            d="M5 12h14m-7-7l7 7l-7 7"
          ></path>
        </svg>
      </a>
    </div>
  </div>
</template>
