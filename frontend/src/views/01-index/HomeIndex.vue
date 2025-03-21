<template>
  <img id="home-img" src="/images/junjiehome.png" />
  <div id="home-content">
      <h1 class="home-container__title">Rubik's Cube</h1>
      <h2 class="home-container__subtitle">With Augmented Reality</h2>

      <nav class="home-container__nav">
        <button class="home-content__button home-content__button--blue" @click="showModal">Instructions</button>
        <a href="http://127.0.0.1:5000" class="home-content__button">Start-in-AR.py</a>
        <router-link to="/scanner" class="home-content__button">Start-in-AR.js</router-link>
        <router-link to="/vr-keyboard" class="home-content__button">Play-in-VR</router-link>
        <a href="/pages/01-ar/ar-buttons.html" class="home-content__button">AR-Buttons.html</a>
      </nav>

      <div v-if="isModalVisible" class="home-container__modal">
        <div class="home-container__modal-content">
          <span class="home-container__modal-close" @click="hideModal">×</span>
          <h2>Program Instructions</h2>
          <p>To start the program, click the "Run Program" button in the center of the home webpage.</p>
          <img class="home-container__modal-image" src="/images/Instruction-arrow.png" alt="Instruction Arrow" />
          <p>
            To use the colour detection program, align the cube with the green dots in the center and click the "Detect Colours" button, then save and next.
            Once you have scanned all six faces, a "Generate Cube" button will appear. Click it to create the cube. If you want to start scanning the cube from the beginning again, press the "Reset Cube" button.
          </p>
          <img class="home-container__modal-image" src="/images/ColourDetectInstructs.png" alt="Colour Detect Instructions" />
        </div>
      </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      isModalVisible: false
    };
  },
  methods: {
    showModal() {
      this.isModalVisible = true;
    },
    hideModal() {
      this.isModalVisible = false;
    }
  }
};
</script>

<style scoped>
#home-img {
  width: 20%;
  height: auto;
  margin-top: 4vh;
  margin-bottom: 4vh;
  margin-inline: 2vw;
}

#home-content {
  flex: 1;
  text-align: center;
  border-radius: 30px;
  box-sizing: border-box;
  margin-inline: 2vh;
  margin-top: clamp(2vh, 1vh, 10%);
  margin-bottom: clamp(2vh, 1vh, 10%);
  padding: 0 !important; /* 强制清除所有 padding */
  height: clamp(2vh, 1vh, 10%);
  overflow-y: auto;
  background-image: url(/images/Rubikcube.jpg);
  background-repeat: repeat;
  background-size: cover;
}

.home-container__title {
  font-size: clamp(45px, 5vw, 100px);
  color: white;
  font-family: "Gochi Hand", cursive;
  text-align: center;
  margin-bottom: 1vh;
}

.home-container__subtitle {
  color: white;
  font-family: "Baloo 2";
  font-size: clamp(20px, 3vw, 40px);
  font-style: normal;
  text-align: center;
  font-weight: 600;
  line-height: 140%;
  margin-bottom: 20px;
}

.home-container__nav ul {
  list-style: none;
  padding: 0;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 10px;
  width: 100%;
}

.home-container__nav li {
  width: 100%;
  text-align: center;
}

.home-content__button {
  background-color: #4CAF50;
  font-family: Arial, sans-serif;
  font-size: clamp(12px, 3vw, 25px);
  font-weight: bold;
  text-decoration: none;
  color: white;
  border-radius: 10px;
  display: flex;
  align-items: center;
  justify-content: center;
  margin: 1% auto;
  width: clamp(250px, 30vw, 300px);
  padding: 10px 20px;
  border: none;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.home-content__button:hover {
  background-color: #4b734e;
}

.home-content__button--blue {
  background-color: #007bff;
  font-size: clamp(15px, 4vw, 30px);
  padding: 10px 20px;
}

.home-content__button--blue:hover {
  background-color: #0056b3;
}

.home-container__modal {
  display: block;
  position: fixed;
  z-index: 1;
  padding-top: 40px;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  overflow: hidden;
  opacity: 0;
  transform: scale(0.9);
  animation: fadeInScale 1s ease forwards;
  background-color: rgba(0, 0, 0, 0.6);
}

.home-container__modal-content {
  background-color: #69e97e;
  margin: auto;
  padding: 20px;
  border: 0.5em solid #000000;
  border-radius: 10px;
  width: 90%;
  max-width: 800px;
  aspect-ratio: unset;
  height: auto;
  max-height: 90vh;
  overflow-y: auto;
  text-align: center;
  font-family: Arial, sans-serif;
}

.home-container__modal-content h2 {
  font-size: clamp(24px, 5vw, 40px);
  font-weight: bold;
  color: #000000;
  margin-bottom: 16px;
}

.home-container__modal-content p {
  font-size: clamp(16px, 3vw, 20px);
  color: #333333;
  line-height: 1.6;
  margin-bottom: 16px;
}

.home-container__modal-close {
  color: #000000;
  float: right;
  margin-right: 0.5em;
  margin-top: 0.5em;
  font-size: 40px;
  font-weight: bold;
  cursor: pointer;
}

.home-container__modal-close:hover {
  color: #ff0000;
}

.home-container__modal-image {
  width: 100%;
  height: auto;
  max-width: 400px;
  margin: 16px auto;
  display: block;
}

@keyframes fadeInScale {
  from {
    opacity: 0;
    transform: scale(0.5);
  }
  to {
    opacity: 1;
    transform: scale(1);
  }
}


@media (max-width: 450px) {
  #home-img {
    width: 40% !important;
    margin: 10px auto !important;
  }

  #home-content {
    padding: 15px !important;
    margin: 10px auto !important;
  }

  .home-container__title {
    font-size: clamp(32px, 9vw, 48px);
  }

  .home-container__subtitle {
    font-size: clamp(18px, 5vw, 28px);
  }

  #home-content p {
    font-size: clamp(14px, 4vw, 18px);
    line-height: 1.6;
  }

  #home-content a,
  .home-content__button {
    width: 90% !important;
    font-size: clamp(16px, 4.5vw, 22px);
    padding: 12px 24px;
  }
}

@media (max-width: 800px) {
  #home-img {
    width: 25% !important;
    margin: 20px auto !important;
  }

  #home-content {
    width: 100%;
    border-radius: 0;
    margin: 20px auto !important;
  }
}
</style>