<script setup lang="ts">
import { slides } from "@/constants";
const currentIndex = ref(0);

const jumpTo = (to: number) => {
  currentIndex.value = to;
};

onMounted(() => {
  const options: IntersectionObserverInit = {
    root: null,
    rootMargin: "0px",
    threshold: 0.1,
  };

  const observer = new IntersectionObserver((entries, observer) => {
    entries.forEach((entry) => {
      const lazyImage = entry.target;
      if (!(lazyImage instanceof HTMLImageElement)) {
        return;
      }
      if (entry.isIntersecting) {
        // todo: 替换 fallback
        lazyImage.src =
          lazyImage.dataset.src ||
          "https://www.peugeot.com.cn/Cg/Upload/www.peugeot.com.cn/image/230529/2023052917174454808.png";
        observer.unobserve(lazyImage);
      }
    });
  }, options);

  const lazyImages = document.querySelectorAll("img[data-src]");
  lazyImages.forEach((image) => {
    observer.observe(image);
  });

  onUnmounted(() => {
    observer.disconnect();
  });
});
</script>

<template>
  <section class="box w-fit">
    <div class="carousel w-96 h-72 mx-auto">
      <div
        class="slide bg-indigo-500"
        :style="{ transform: `translateX(-${currentIndex * 100}%)` }"
      >
        <div
          v-for="(item, index) in slides"
          :key="index"
          class="slide-item w-full h-full"
        >
          <img
            :alt="item.caption"
            loading="lazy"
            :data-src="item.image"
            :src="index === 0 ? item.image : ''"
          />
          <div class="caption">{{ item.caption }}</div>
        </div>
      </div>
      <div class="controls">
        <button v-for="(item, index) in slides" @click="() => jumpTo(index)">
          {{ item.caption }}
        </button>
      </div>
    </div>
  </section>
</template>

<style scoped>
.carousel {
  @apply relative overflow-hidden;
}

.slide {
  @apply flex transition-transform duration-300 ease-in-out;
}

.slide-item {
  @apply relative flex-none w-full;
}

img {
  @apply w-full h-full object-cover;
}

.caption {
  @apply absolute bottom-10 left-10 text-white;
}

.controls {
}

button {
  @apply ml-10;
}
</style>
