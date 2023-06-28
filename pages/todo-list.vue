<script setup lang="tsx">
type Item = {
  id: string;
  value: string;
};

const SAMPLE_ITEM = { id: "xxx", value: "这是一个样例" };

const inputValue = ref("");
const items = ref<Item[]>([SAMPLE_ITEM]);
const handleConfirmAdd = () => {
  // mutation methods 操作 reactive array
  // https://vuejs.org/guide/essentials/list.html#array-change-detection
  items.value.push({
    id: "sd",
    value: inputValue.value,
  });
};

// https://nuxt.com/docs/getting-started/assets#global-styles-imports
</script>
<template>
  <section class="bg-white p-4 w-96 space-y-4 shadow min-h-[200px] rounded-lg">
    <form class="flex item-center gap-2" @submit.prevent="handleConfirmAdd">
      <input
        type="text"
        class="flex-1 w-12 nui-focus border-slate-300 text-slate-600 placeholder:text-slate-300 dark:border-slate-700 dark:bg-slate-900/75 dark:text-slate-200 dark:placeholder:text-slate-500 dark:focus:border-slate-700 peer border bg-white font-sans transition-all duration-300 disabled:cursor-not-allowed disabled:opacity-75 px-2 h-10 py-2 text-sm leading-5 pe-4 ps-9 rounded-xl h-12 text-base !ps-6"
        placeholder="在这里输入内容"
        v-model="inputValue"
      />
      <Button type="submit" class="!w-16">添加</Button>
    </form>
    <div class="p-2">
      <ListItem
        v-for="item in items"
        :title="item.value"
        :description="item.value.split('').reverse().join('')"
        :initial="item.value.slice(0, 1)"
      />
    </div>
  </section>
</template>
