<script setup lang='ts'>
import {onMounted, ref, useTemplateRef} from 'vue'

    const showMenu = ref(false);
    const transparentHeader = ref(true);

    function toggleShowMenu() {
        showMenu.value = !showMenu.value;
    }

    onMounted(() => {
        const bottomMarker = useTemplateRef("header-bottom-marker");
        const observer = new IntersectionObserver(([entry]) => {
            transparentHeader.value = entry.isIntersecting;
        });

        if (bottomMarker.value) {
          observer.observe(bottomMarker.value);
        }
    });

</script>
<template>
  <div id="header"
       class="fixed w-full flex justify-center items-center
        {{ !!transparentHeader && !showMenu ? 'bg-transparent' : 'bg-stone-500' }}"
  >
    <nav class="container flex items-start justify-between flex-wrap
            {{ !!transparentHeader && !showMenu ? 'text-stone-900' : 'text-stone-200'}}
            font-mono p-6">
      <div class="flex items-center flex-shrink-0 mr-6">
        <svg class="fill-current h-8 w-8 mr-2" width="54" height="54" viewBox="0 0 54 54" xmlns="http://www.w3.org/2000/svg"><path d="M13.5 22.1c1.8-7.2 6.3-10.8 13.5-10.8 10.8 0 12.15 8.1 17.55 9.45 3.6.9 6.75-.45 9.45-4.05-1.8 7.2-6.3 10.8-13.5 10.8-10.8 0-12.15-8.1-17.55-9.45-3.6-.9-6.75.45-9.45 4.05zM0 38.3c1.8-7.2 6.3-10.8 13.5-10.8 10.8 0 12.15 8.1 17.55 9.45 3.6.9 6.75-.45 9.45-4.05-1.8 7.2-6.3 10.8-13.5 10.8-10.8 0-12.15-8.1-17.55-9.45-3.6-.9-6.75.45-9.45 4.05z"/></svg>
        <span class="font-semibold text-xl ">Website</span>
      </div>

      <div class="hidden md:block md:flex md:items-center md:justify-end md:w-auto">
        <div class="text-lg">
          <a href="/" class="block mt-4 md:inline-block md:mt-0 mr-4 hover:underline decoration-2">
            Home
          </a>
          <a href="/about/" class="block mt-4 md:inline-block md:mt-0 mr-4 hover:underline decoration-2">
            About
          </a>
          <a href="/blog/" class="block mt-4 md:inline-block md:mt-0 hover:underline decoration-2">
            Blog
          </a>
        </div>
      </div>

      <div class="block w-100 md:hidden">
        <div class="flex flex-col items-end justify-start">
          <button class="block items-center px-3 py-2 "
                  @click='toggleShowMenu' >
            <svg class="fill-current h-5 w-5" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg"><title>Menu</title><path d="M0 3h20v2H0V3zm0 6h20v2H0V9zm0 6h20v2H0v-2z"/></svg>
          </button>
          <div v-if='showMenu' class="flex flex-col text-lg self-start text-right">
            <a href="/" class=" mt-4">
              Home
            </a>
            <a href="/about/" class=" mt-4">
              About
            </a>
            <a href="/blog/" class=" mt-4">
              Blog
            </a>
          </div>
        </div>
      </div>
    </nav>
  </div>
  <div ref="header-bottom-marker"></div>

</template>