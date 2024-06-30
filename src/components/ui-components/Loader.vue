<template>
  <div class="loader"></div>
</template>

<script>
export default {
  name: "Loader",
};
</script>

<style>
.loader {
  position: relative;
  width: 0;
  height: 0;
  margin: 4rem auto;
  animation: anim-rotate 1.2s infinite ease;
  padding: 1rem;
}

.loader::before,
.loader::after {
  content: "";
  position: absolute;
  width: 20px;
  height: 20px;
  top: 50%;
  left: 50%;
  margin-top: -10px; /* @ball-size / 2 */
  margin-left: -10px; /* @ball-size / 2 */
  border-radius: 10px; /* @ball-size / 2 */
  opacity: 0.9;
}

.loader::before {
  background: #00a7ce; /* @color-1 */
  transform: translate(-0.75em, -0.75em) scale(1); /* @jump */
  box-shadow: 1.5em 1.5em 0 #72c45a; /* @diam */
  animation: anim-1-2 1.2s infinite ease;
}

.loader::after {
  background: #f963a3; /* @color-3 */
  transform: translate(0.75em, -0.75em) scale(1); /* @jump */
  box-shadow: -1.5em 1.5em 0 #ffd15b; /* @diam */
  animation: anim-3-4 1.2s infinite ease;
}

@keyframes anim-1-2 {
  50% {
    transform: scale(1.3) translate(0, 0);
    box-shadow: 0 0 0 #72c45a; /* @color-2 */
    opacity: 0.8;
  }
}

@keyframes anim-3-4 {
  50% {
    transform: scale(1.3) translate(0, 0);
    box-shadow: 0 0 0 #ffd15b; /* @color-4 */
    opacity: 0.8;
  }
}

@keyframes anim-rotate {
  0% {
    transform: rotate(0deg);
  }
  50% {
    transform: rotate(360deg);
  }
  100% {
    transform: rotate(720deg);
  }
}
</style>
