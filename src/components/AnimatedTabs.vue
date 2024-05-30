<template>
  <div class="wrapp">
    <div class="header">
      <div class="header__b1">
        <div
          v-for="(tab, index) in tabs"
          :key="index"
          :class="['tab__b1', { active: activeIndex === index }]"
          ref="tabB1"
        >
          <div class="tab__b1-text" ref="tabB1Text">
            <div class="tab__b1-row">{{ tab.title }}</div>
            <div class="tab__b1-row">{{ tab.subtitle }}</div>
          </div>
          <img :src="tab.image" alt="" />
        </div>
      </div>
      <div class="header__footer">
        <div class="header__footer-wrapp">
          <div class="header__footer-txt"></div>
          <ul class="tab">
            <li
              v-for="(tab, index) in tabs"
              :key="index"
              :class="['tab__item', { active: activeIndex === index }]"
              @click="() => changeTab(index)"
            >
              <div class="tab__item-img">
                <img :src="tab.image" alt="" />
              </div>
              <div
                class="tab__item-shadow"
                :style="{ backgroundImage: 'url(' + tab.image + ')' }"
              ></div>
            </li>
          </ul>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { gsap, Power4 } from "gsap";

export default {
  data() {
    return {
      tabs: [
        {
          title: "astronaut",
          subtitle: "on the mars",
          image:
            "https://images.unsplash.com/photo-1716718405882-5d80d89ea24e?q=80&w=2787&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D",
        },
        {
          title: "astronaut",
          subtitle: "on the earth",
          image:
            "https://images.unsplash.com/photo-1716847214612-e2c2f3771d41?q=80&w=2667&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D",
        },
        {
          title: "astronaut",
          subtitle: "on the moon",
          image:
            "https://images.unsplash.com/photo-1716724827706-82b216af4f94?q=80&w=2787&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D",
        },
      ],
      activeIndex: 0,
    };
  },
  methods: {
    changeTab(index) {
      if (this.activeIndex !== index) {
        let previousIndex = this.activeIndex;
        this.activeIndex = index;

        const tabB1Elements = this.$refs.tabB1;
        const tabB1TextElements = this.$refs.tabB1Text;

        gsap.to(tabB1Elements[previousIndex], {
          duration: 0.3,
          opacity: 0,
          x: -100,
          onComplete: () => {
            gsap.set(tabB1Elements[previousIndex], { display: "none" });
            gsap.set(tabB1Elements[this.activeIndex], { display: "block" });

            gsap.fromTo(
              tabB1Elements[this.activeIndex],
              { x: 100, opacity: 0 },
              { duration: 0.5, x: 0, opacity: 1, ease: Power4.easeOut }
            );
            gsap.fromTo(
              tabB1TextElements[this.activeIndex],
              { x: 100, opacity: 0 },
              {
                duration: 0.5,
                delay: 0.1,
                x: 0,
                opacity: 1,
                ease: Power4.easeOut,
              }
            );
          },
        });
      }
    },
  },
};
</script>

<style scoped>
@import url("../assets/css/styles.css");
</style>
