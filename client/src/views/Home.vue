<template>
  <div class="home">
    <div class="container">
      <div class="free-poker-header">
        <h1>Scrum poker made simple and <span>free</span>.</h1>
      </div>
      <div class="start-game">
        <button
          class="button"
          :class="{ disabled: clickedStart }"
          @click="startGame()"
        >
          <span v-if="!clickedStart">Start new game</span>

          <svg
            v-if="clickedStart"
            version="1.1"
            id="Layer_1"
            xmlns="http://www.w3.org/2000/svg"
            xmlns:xlink="http://www.w3.org/1999/xlink"
            x="0px"
            y="0px"
            width="24px"
            height="30px"
            viewBox="0 0 24 30"
            style="enable-background: new 0 0 50 50"
            xml:space="preserve"
          >
            <rect x="0" y="10" width="4" height="10" fill="#333" opacity="0.2">
              <animate
                attributeName="opacity"
                attributeType="XML"
                values="0.2; 1; .2"
                begin="0s"
                dur="0.6s"
                repeatCount="indefinite"
              />
              <animate
                attributeName="height"
                attributeType="XML"
                values="10; 20; 10"
                begin="0s"
                dur="0.6s"
                repeatCount="indefinite"
              />
              <animate
                attributeName="y"
                attributeType="XML"
                values="10; 5; 10"
                begin="0s"
                dur="0.6s"
                repeatCount="indefinite"
              />
            </rect>
            <rect x="8" y="10" width="4" height="10" fill="#333" opacity="0.2">
              <animate
                attributeName="opacity"
                attributeType="XML"
                values="0.2; 1; .2"
                begin="0.15s"
                dur="0.6s"
                repeatCount="indefinite"
              />
              <animate
                attributeName="height"
                attributeType="XML"
                values="10; 20; 10"
                begin="0.15s"
                dur="0.6s"
                repeatCount="indefinite"
              />
              <animate
                attributeName="y"
                attributeType="XML"
                values="10; 5; 10"
                begin="0.15s"
                dur="0.6s"
                repeatCount="indefinite"
              />
            </rect>
            <rect x="16" y="10" width="4" height="10" fill="#333" opacity="0.2">
              <animate
                attributeName="opacity"
                attributeType="XML"
                values="0.2; 1; .2"
                begin="0.3s"
                dur="0.6s"
                repeatCount="indefinite"
              />
              <animate
                attributeName="height"
                attributeType="XML"
                values="10; 20; 10"
                begin="0.3s"
                dur="0.6s"
                repeatCount="indefinite"
              />
              <animate
                attributeName="y"
                attributeType="XML"
                values="10; 5; 10"
                begin="0.3s"
                dur="0.6s"
                repeatCount="indefinite"
              />
            </rect>
          </svg>
        </button>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";

import { io } from "socket.io-client";
import store from "@/store";
import router from "@/router";
@Component({
  components: {},
})
export default class Home extends Vue {
  public clickedStart = false;
  public startGame() {
    this.clickedStart = true;

    const socket = io(process.env.VUE_APP_SERVER);
    store.commit("setSocket", socket);
    store.state.socket.on("room", (roomId: string) => {
      router.push({ path: `game/${roomId}` });
    });
  }
}
</script>

<style scoped lang="scss">
.home {
  display: flex;
  justify-content: center;
  height: 100%;
  width: 100%;
  box-sizing: border-box;
}


.container {
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: center;
  width: 800px;
}

.free-poker-header {
  display: flex;
  align-items: center;
  justify-content: center;
  position: relative;
  height: 80%;
  width: 100%;
  h1 {
    user-select: none;
    font-size: 3.2em;
    span {
      color: #54e8dd;
      text-decoration: underline;
    }
  }
}

.start-game {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 100%;
  height: 80%;
  position: relative;
}
.button {
  user-select: none;
  display: flex;
  align-items: center;
  justify-content: center;
  position: absolute;
  z-index: 9999;
  width: 320px;
  height: 80px;
  background: #f3f0f1;
  border-radius: 32px;
  text-align: center;
  border: none;
  cursor: pointer;
  transition: all 0.1s ease-in-out;
  box-shadow: -6px -6px 10px rgba(255, 255, 255, 0.8),
    6px 6px 10px rgba(0, 0, 0, 0.2);
  color: #161b1f;
  &:hover {
    opacity: 0.3;
    box-shadow: -6px -6px 10px rgba(255, 255, 255, 0.8),
      6px 6px 10px rgba(0, 0, 0, 0.2);
  }
  &:active {
    opacity: 1;
    box-shadow: inset -4px -4px 8px rgba(255, 255, 255, 0.5),
      inset 8px 8px 16px rgba(0, 0, 0, 0.1);
  }
  &:focus {
    outline: none;
  }

  span {
    line-height: 100px;
    font-family: "Montserrat", sans-serif;
    font-size: 26px;
    font-weight: semibold;
  }
}

.disabled {
  opacity: 1;
  box-shadow: inset -4px -4px 8px rgba(255, 255, 255, 0.5),
    inset 8px 8px 16px rgba(0, 0, 0, 0.1);

  &:hover {
    opacity: 1;
    box-shadow: inset -4px -4px 8px rgba(255, 255, 255, 0.5),
      inset 8px 8px 16px rgba(0, 0, 0, 0.1);
  }
}

svg rect {
  fill: #54e8dd;
}


@media only screen and (max-width: 800px) {
  
  .container {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    width: 800px;
  }

  .free-poker-header {
    width: 90%;
    align-items: flex-end;
  }

  .start-game {
    align-items: flex-start;
  }
}
</style>
