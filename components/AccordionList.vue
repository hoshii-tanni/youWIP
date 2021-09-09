<template>
  <dl class="accordion flex flex-col-reverse">
    <dt @click="click" class="title flex justify-center mt-1">
      <i class="bi bi-chevron-down flex justify-center items-end text-gray-500 text-xl"></i>
    </dt>
    <dd style="display:none;" class="inner">
      <slot />
    </dd>
  </dl>
</template>

<script>
import Vue from 'vue'

export default Vue.extend({
  props: {
    
  },
  methods:{
    slideUp(el, duration=300) {
      el.style.height = el.offsetHeight + "px";
      el.offsetHeight;
      el.style.transitionProperty = "height, margin, padding";
      el.style.transitionDuration = duration + "ms";
      el.style.transitionTimingFunction = "ease";
      el.style.overflow = "hidden";
      el.style.height = "0";
      el.style.paddingTop = "0";
      el.style.paddingBottom = "0";
      el.style.marginTop = "0";
      el.style.marginBottom = "0";
      setTimeout(() => {
        el.style.display = "none";
        el.style.removeProperty("height");
        el.style.removeProperty("padding-top");
        el.style.removeProperty("padding-bottom");
        el.style.removeProperty("margin-top");
        el.style.removeProperty("margin-bottom");
        el.style.removeProperty("overflow");
        el.style.removeProperty("transition-duration");
        el.style.removeProperty("transition-property");
        el.style.removeProperty("transition-timing-function");
        el.classList.remove("is-open");
      }, duration);
    },

    slideDown(el, duration = 300) {
      el.classList.add("is-open");
      el.style.removeProperty("display");
      let display = window.getComputedStyle(el).display;
      if (display === "none") {
        display = "block";
      }
      el.style.display = display;
      let height = el.offsetHeight;
      el.style.overflow = "hidden";
      el.style.height = "0";
      el.style.paddingTop = "0";
      el.style.paddingBottom = "0";
      el.style.marginTop = "0";
      el.style.marginBottom = "0";
      el.offsetHeight;
      el.style.transitionProperty = "height, margin, padding";
      el.style.transitionDuration = duration + "ms";
      el.style.transitionTimingFunction = "ease";
      el.style.height = height + "px";
      el.style.removeProperty("padding-top");
      el.style.removeProperty("padding-bottom");
      el.style.removeProperty("margin-top");
      el.style.removeProperty("margin-bottom");
      setTimeout(() => {
        el.style.removeProperty("height");
        el.style.removeProperty("overflow");
        el.style.removeProperty("transition-duration");
        el.style.removeProperty("transition-property");
        el.style.removeProperty("transition-timing-function");
      }, duration);
    },

    slideToggle(target, el, duration = 300) {
      if (window.getComputedStyle(el).display === "none") {
        target.classList.add("open")
        this.slideDown(el, duration);
      } else {
        target.classList.remove("open")
        return this.slideUp(el, duration);
      }
    },

    click(vl) {
      //console.log((<HTMLElement>vl.target).parentNode)
      let target = vl.target;

      while(target.nodeName != "DT") {
        target = target.parentNode;
      }

      const sibling = target.nextElementSibling;
      this.slideToggle(target, sibling);
    },

  },
})
</script>

<style lang="scss">
.accordion {
  .title {
    display: flex;
    padding: 0 2px;

    &.open i {transform:rotate(180deg);}
  }
}

</style>