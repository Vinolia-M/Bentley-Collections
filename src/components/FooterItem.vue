<template>
  <div class="item">
    <div class="details">
      <h3>
        <slot name="heading"></slot>
      </h3>
      <slot></slot>
    </div>
    <div class="social-icons">
        <slot name="icon"></slot>
      </div>
  </div>
</template>

<style scoped>
.item {
  position: fixed;
  bottom: 40px;
  right: 9%;
  z-index: -1;
  display: flex;
  gap: 50px;
  justify-content: end;
  align-items: center;
}

.social-icons {
    display: flex;
    gap: 20px;
    cursor: pointer;
  }

h3 {
  font-size: 16px;
  font-weight: 500;
}

@media screen and (max-width: 510px) {
  .item {
    justify-content: center;
    width: 80%;
}
}
</style>
