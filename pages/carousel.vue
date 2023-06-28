<script setup lang="ts">
import { slides } from "@/constants";
const currentIndex = ref(0);

const jumpTo = (to: number) => {
  currentIndex.value = to;
};

const imageLoadedArr = ref(slides.map((e) => false));

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

  const lazyImages = document.querySelectorAll(
    "img[data-src]"
  ) as NodeListOf<HTMLImageElement>;

  lazyImages.forEach((image, index) => {
    image.addEventListener("load", () => {
      imageLoadedArr.value[index] = true;
    });
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
        class="slide"
        :style="{ transform: `translateX(-${currentIndex * 100}%)` }"
      >
        <div
          v-for="(item, index) in slides"
          :key="index"
          class="slide-item bg-slate-200"
        >
          <div
            class="absolute inset-0 flex justify-center items-center text-slate-700"
            v-show="!imageLoadedArr[index]"
          >
            加载中...
          </div>
          <img
            :alt="item.caption"
            loading="lazy"
            :data-src="item.image"
            :class="{
              'opacity-0': !imageLoadedArr[index],
            }"
          />
          <div class="caption" v-show="!!imageLoadedArr[index]">
            {{ item.caption }}
          </div>
        </div>
      </div>
    </div>
    <div class="controls">
      <button v-for="(item, index) in slides" @click="() => jumpTo(index)">
        {{ index }}
      </button>
    </div>
  </section>
</template>

<style scoped>
.carousel {
  @apply relative overflow-hidden;
}

.slide {
  @apply flex transition-transform duration-300 ease-in-out h-full;
}

.slide-item {
  @apply relative flex-none w-full h-full;
}

img {
  @apply w-full h-full object-cover;
}

.caption {
  @apply absolute bottom-4 left-0 right-0 text-center text-white;
}

.controls {
}

button {
  @apply ml-10;
}
</style>
