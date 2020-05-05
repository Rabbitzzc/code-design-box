> 利用 animation 创建 bouncing loader 动画

```html run
<template>
  <div class="bouncing-loader">
  <div></div>
  <div></div>
  <div></div>
</div>
</template>
<style scoped>
  .bouncing-loader {
      display:flex;
      justify-content: center;
  }
  .bouncing-loader > div {
      width: 1rem;
      height: 1rem;
      margin: 3rem 0.2rem;
      border-radius:50%;
      background: #ff5200;
      /* alternate 循环前后 */
      animation: bouncing-loader 0.6s infinite alternate;
  }

  .bouncing-loader > div:nth-child(2) {
      animation-delay: 0.2s;
  }
  .bouncing-loader > div:nth-child(3) {
      animation-delay: 0.4s;
  }

  @keyframes bouncing-loader {
      0% {
          opacity: 1;
          transform: translateY(0);
      }
      100% {
          opacity:0.1;
          transform: translateY(-1rem);
      }
  }
</style>
```