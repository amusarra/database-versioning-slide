<template>
  <div class="slidev-layout default">
    <slot />
  </div>
</template>

<style lang="postcss">
.slidev-layout.default {
  background-image: url("../images/background_slide_1.png");
  background-repeat: no-repeat;
  background-position: center;
  background-size: cover;
  padding: 2em 2em;
}
</style>