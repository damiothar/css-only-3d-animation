<template>
  <div
    id="app"
    :style="`
      --ballColor: ${ballColor};
      --ballOpacity: ${ballOpacity};
      --cubeColor: ${cubeColor};
      --cubeOpacity: ${cubeOpacity};
    `"
  >
    <Phone :shadows="shadows" :animation="animation" />
    <div class="options">
      <!-- General -->
      <h2 class="options__title">General</h2>
      <div class="field">
        <label class="field__control" for="animation">
          <input
            id="animation"
            class="field__input --checkbox"
            type="checkbox"
            v-model="animation"
          />
          Animation
        </label>
      </div>
      <div class="field">
        <label class="field__control" for="shadows">
          <input
            id="shadows"
            class="field__input --checkbox"
            type="checkbox"
            v-model="shadows"
          />
          Shadows
        </label>
      </div>

      <!-- Ball -->
      <h2 class="options__title">Ball</h2>
      <div class="field">
        <label
          class="field__control --color"
          for="ballColor"
          :style="`--color: ${ballColor}`"
        >
          Color
          <input
            id="ballColor"
            class="field__input --color"
            type="color"
            v-model="ballColor"
          />
        </label>
      </div>
      <div class="field">
        <div class="field__control">Alpha</div>
        <input
          class="field__input --range"
          type="range"
          min="0.4"
          max="1"
          step="0.01"
          v-model="ballOpacity"
        />
      </div>

      <!-- Cube -->
      <h2 class="options__title">Cube</h2>
      <div class="field">
        <label
          class="field__control --color"
          for="cubeColor"
          :style="`--color: ${cubeColor}`"
        >
          Color
          <input
            id="cubeColor"
            class="field__input --color"
            type="color"
            v-model="cubeColor"
          />
        </label>
      </div>
      <div class="field">
        <div class="field__control">Alpha</div>
        <input
          class="field__input --range"
          type="range"
          min="0.2"
          max="0.8"
          step="0.01"
          v-model="cubeOpacity"
        />
      </div>
      <div class="copy">
        by
        <a
          class="copy__link"
          href="https://github.com/damiothar"
          target="_blank"
          >Damian Othar</a
        >
      </div>
    </div>
  </div>
</template>



<script>
import Phone from '@/components/Phone';

export default {
  name: 'App',
  components: {
    Phone
  },
  data() {
    return {
      shadows: true,
      animation: true,

      ballColor: '#00ffb7',
      ballOpacity: 1,
      cubeColor: '#ff00ea',
      cubeOpacity: 0.5
    };
  }
};
</script>



<style lang="scss">
// Resets
@import '~normalize-scss/sass/normalize';
@include normalize();
* {
  box-sizing: border-box;
  user-select: none;
}
// ***************************************************************
// Variables
:root {
  --rotateSpeed: 30s;
  --bounceSpeed: 1.5s;
  --floorColorDark: #1f1d38;
  --floorColorLight: #4c4a6b;
  --backgroundColor: #0d0b24;
}
#app {
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  position: relative;
  background-image: 
    linear-gradient(-45deg, #0009, #0006),
    linear-gradient(-45deg, var(--cubeColor), var(--ballColor));
  color: #fff;
  font-family: sans-serif;
}
// ***************************************************************
.options {
  background-color: #fff1;
  padding: 20px;
  border-radius: 6px;
  position: absolute;
  right: 12px;
  top: 12px;
}
.options__title {
  font-size: 12px;
  text-transform: uppercase;
  letter-spacing: 3px;
  line-height: 1;
  font-weight: 400;
  color: #fff9;
  border-bottom: 1px solid #fff2;
  padding-bottom: 6px;
  margin: 30px 0 12px;
  &:first-child {
    margin-top: 0;
  }
}
// ***************************************************************
$colorSize: 13px;
.field {
  + .field {
    margin-top: 10px;
  }
}
.field__control {
  cursor: pointer;
  user-select: none;
  font-size: 14px;
  line-height: 1;
  position: relative;
  &.--color {
    position: relative;
    &::after {
      content: '';
      background-color: var(--color);
      display: inline-block;
      width: $colorSize;
      height: $colorSize;
      border: 1px solid #fffa;
      border-radius: 2px;
      margin-left: 5px;

      position: absolute;
      top: 0;
      right: 0;
    }
  }
}
.field__input {
  cursor: pointer;
  &.--checkbox {
    margin-right: 5px;
  }
  &.--color {
    opacity: 0;
    margin-left: 2px;
    width: $colorSize;
    height: $colorSize;
    border: none;
  }
  &.--range {
    margin-top: 10px;
    width: 140px;
    height: 8px;
  }
}
.copy {
  color: #fffc;
  position: absolute;
  top: 100%;
  right: 5px;
  margin-top: 15px;
  font-size: 12px;
  &__link {
    color: inherit;
    &:hover {
      color: #fff;
    }
  }
}
</style>