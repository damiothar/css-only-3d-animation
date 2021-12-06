<template>
  <label
    class="phone"
    :class="[shadows ? '--hasShadows' : '', animation ? '--hasAnimation' : '']"
    for="animation"
  >
    <div class="viewport">
      <!-- Title -->
      <h1 class="title">
        <div class="title__line">
          <span class="title__css">CSS </span
          ><span class="title__only">Only</span>
        </div>
        <div class="title__line">3D Animation</div>
      </h1>
      <!-- Scene -->
      <div class="scene">
        <div class="floor"></div>
        <div class="cube">
          <div class="cube__side --front"></div>
          <div class="cube__side --back"></div>
          <div class="cube__side --left"></div>
          <div class="cube__side --right"></div>
          <div class="cube__side --top">
            <div class="ball__shadow"></div>
          </div>
          <div class="cube__side --bottom"></div>
        </div>
        <div class="ball"></div>
      </div>
      <!-- Pause -->
      <div class="pause">
        <div class="pause__icon"></div>
      </div>
    </div>
  </label>
</template>



<script>
export default {
  name: 'Scene',
  props: {
    shadows: Boolean,
    animation: Boolean
  }
};
</script>



<style lang="scss">
// Keyframes
@keyframes sceneRotate {
  to { transform: rotateY(360deg); }
}
@keyframes ballBounce {
  0%,
  100% { bottom: .5em; }
  50% { bottom: 3em; animation-timing-function: ease-in; }
}
@keyframes ballShadow {
  0%,
  93.5%,
  100% {  transform: scale(1.5); opacity: 1; }
  50% { transform: scale(1); opacity: 0.5; animation-timing-function: ease-in; }
}
@keyframes cubeHeight {
  0%,
  100% { height: 1.5em; }
  8%,
  93.5% { height: 2em; }
}
// ***************************************************************
.phone {
  cursor: pointer;
  width: 320px;
  max-width: 80vw;
  aspect-ratio: 9 / 18;
  border-radius: 25px;
  overflow: hidden;
  box-shadow:
    // Edges
    1px 1px 3px #fff2, 2px 2px 3px #fff2, 3px 3px 3px #fff2,
    6px 6px 0px 3px #fff2,
    // Outer Shadow
    20px 20px 30px #0005;
    // Animations
  * {
    animation-play-state: paused !important;
  }
  &.--hasAnimation * {
    animation-play-state: running !important;
  }
}
// ***************************************************************
.viewport {
  width: 100%;
  height: 100%;
  position: relative;
  font-size: 70px;
  background-color: var(--backgroundColor);
  // Camera distance
  perspective: 10em;
  // Camera angle
  perspective-origin: 50% calc(50% - 2em);
}
// ***************************************************************
.title {
  font-size: .28em;
  font-weight: 600;
  letter-spacing: .05em;
  line-height: 1.6;
  color: #fffd;
  text-transform: uppercase;
  text-align: center;
  position: absolute;
  top: 2em;
  left: 50%;
  transform: translateX(-50%);
  z-index: 1;
  &__line {
    white-space: nowrap;
  }
  &__css {
    color: var(--ballColor);
  }
  &__only {
    color: var(--cubeColor);
  }
}
// ***************************************************************
.scene {
  position: absolute;
  top: 68%;
  left: 50%;
  transform-style: preserve-3d;
  animation: sceneRotate var(--rotateSpeed) infinite linear;
}
// ***************************************************************
.ball {
  width: 1em;
  height: 1em;
  border-radius: 50%;
  background-color: var(--ballColor);
  opacity: var(--ballOpacity);
  position: absolute;
  left: -0.5em;
  bottom: 1em;
  transform-style: preserve-3d;
  animation:
    ballBounce var(--bounceSpeed) infinite ease-out,
    sceneRotate var(--rotateSpeed) infinite linear reverse;
}
.--hasShadows .ball {
  background-image:
  // Ambient oclusion
    radial-gradient(circle at top, var(--ballColor), #000);
}

.ball__shadow {
  position: absolute;
  width: 100%;
  height: 100%;
  animation: ballShadow var(--bounceSpeed) infinite ease-out;
}
.--hasShadows .ball__shadow {
  background-image: radial-gradient(#000, #0000 25%);
}

// ***************************************************************
.cube {
  width: 2em;
  height: 2em;
  position: absolute;
  bottom: -1em;
  left: -1em;
  transform-style: preserve-3d;
  animation: cubeHeight var(--bounceSpeed) infinite linear;
}

.cube__side {
  position: absolute;
  background-color: var(--cubeColor);
  opacity: var(--cubeOpacity);
  &.--left,
  &.--right,
  &.--front,
  &.--back {
    width: 100%;
    height: 100%;
  }
  &.--front {
    transform: translateZ(1em);
  }
  &.--right {
    transform: rotateY(90deg) translateZ(1em);
  }
  &.--back {
    transform: rotateY(180deg) translateZ(1em);
  }
  &.--left {
    transform: rotateY(270deg) translateZ(1em);
  }
  &.--top,
  &.--bottom {
    width: 2em;
    height: 2em;
  }
  &.--top {
    transform: translateY(-50%) rotateX(90deg);
  }
  &.--bottom {
    bottom: 0;
    transform: translateY(50%) rotateX(90deg);
  }
}
.--hasShadows .cube__side {
  &.--left,
  &.--right,
  &.--front,
  &.--back,
  &.--top {
    box-shadow: 0 0 0.5em #000a inset;
  }
  &.--bottom {
    background-color: #0007;
    box-shadow: 0 0 0.5em #000a;
  }
}
// ***************************************************************
.floor {
  width: 15em;
  height: 15em;
  background-image:
    // Tiles
    radial-gradient(#0000, #0000 75%),
    repeating-conic-gradient(from 45deg, var(--floorColorDark) 0deg 90deg, var(--floorColorLight) 90deg 180deg);
  background-size: 100%, 1em 1em;
  position: absolute;
  top: 1em;
  transform: translate(-50%, -50%) rotateX(90deg);
}
.--hasShadows .floor {
  background-image:
    // Tiles
    radial-gradient(#0000, var(--backgroundColor) 75%),
    repeating-conic-gradient(from 45deg, var(--floorColorDark) 0deg 90deg, var(--floorColorLight) 90deg 180deg);
}
// ***************************************************************
.pause {
  $pauseSize: .8em;
  $pauseColor: #fff9;
  position: absolute;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  z-index: 1000;
  background-color: #0008;
  display: flex;
  justify-content: center;
  align-items: center;
  transition: opacity .3s ease;
  &__icon {
    position: absolute;
    width: $pauseSize;
    height: $pauseSize;
    background-image: linear-gradient(
      90deg,
      $pauseColor 40%,
      transparent 40% 60%,
      $pauseColor 60%,
    );
    transform: scale(.9);
    transition: opacity .3s ease;
  }
}
.phone.--hasAnimation .pause {
  opacity: 0;
}
</style>