<style>
.container {
  height: 100%;
  width: 100%;
  position: relative;
  overflow: hidden;
}
.wheel-cont {
  height: 100vh;
  width: 100vh;
  position: absolute;
  left: -50vh;
  transform: rotate(90deg);
}
.copy-cont {
  position: absolute;
  top: 0;
  left: 50vh;
  right: 0;
  padding: 20px 0;
  text-align: center;
}
.card-cont {
  position: absolute;
  top: 150px;
  left: 50vh;
  right: 0;
  padding: 15px;
}
.button {
  font-family: 'Geogrotesque' !important;
  display: inline-block;
  padding: 5px 15px;
  font-size: 20px;
  border-radius: 2px;
  margin: 30px 0;
  cursor: pointer;
  color: white;
  background: #FF0080;
}
.button:hover {
  transition: .5s;
  color: white;
  background: #E622A5;
}
.small {
  font-size: 16px;
  text-decoration: none;
  margin: 15px 0 0;
}
.card {
  border: 2px solid #333333;
  border-radius: 2px;
  text-align: center;
  max-width: 300px;
  margin: 0 auto;
  font-family: 'Geogrotesque Regular';
  background: white;
}
.quest {
  font-size: 100px;
  margin: 30px 0;
}

h2 {
  font-size: 30px;
}

.spin {
  position: absolute;
  top: 120px;
  transform: translateY(-50%);
  margin: 0 auto;
  max-width: 200px;
  left: 0;
  right: 0;
  transition: top .5s linear;
}

.start {
  top: 50vh;
  transition: top .5s linear;
}

.card-wrap {
  padding: 15px;
}
.img {
  height: 125px;
  background-size: cover;
  background-position: center center;
}

.mobile {
  display: none;
}

@media (max-aspect-ratio: 2/3) {
  h2 {
    font-size: 20px;
  }
  .button {
    font-size: 14px;
  }
  .spin {
    position: absolute;
    top: 50vw;
    transform: translateY(-50%);
    margin: 0 auto;
    left: 10px;
    right: 10px;
  }
  .card-cont {
    top: 100vw;
    left: 0;
    right: 0;
  }
  .card-wrap {
    font-size: 0.8em;
  }
  .img {
    height: 80px;
  }

  .mobile {
    display: block;
  }

  .wheel-cont {
    height: 100vw;
    width: 100vw;
    left: -50vw;
  }

  .copy-cont {
    left: 50vw;
  }
  .card-cont {
    padding-top: 0;
  }
  .start {
    top: 50vw;
    transition: top .5s linear;
  }

}
.fade-enter-active, .fade-leave-active {
  transition: opacity .5s;
}
.fade-enter, .fade-leave-to {
  opacity: 0;
}

</style>

<template>
  <div class="container">
    <!-- <img v-for="o in options" :src="require(`@/assets/img/${ o.img }`)" /> -->
    <div class="copy-cont">
      <h2>
        WYLOSUJ
        <br class="mobile" />
        WYZWANIE
      </h2>
      <div class="button spin" :class="{ start: first }" @click.prevent="spin">{{ losuj }}</div>
    </div>
    <div class="card-cont">
      <transition name="fade">
        <div v-if="card" class="card">
          <div class="img" :style="{ backgroundImage: 'url(' + require(`@/assets/img/${ card.img }`) + ')' }" />
          <div class="card-wrap">
            <h3>{{ card.name.toUpperCase() }}</h3>
            <br />
            {{ card.quest }}
            <br />
            <a class="button small" :href="card.href" target="_blank">DOWIEDZ SIĘ WIĘCEJ</a>
          </div>
        </div>
      </transition>
    </div>
    <div class="wheel-cont">
      <Wheel
        ref="wheel"
        :options="options"
        :singleWin="true"
        :removeWin="true"
        @result="result" />
    </div>
  </div>
</template>

<script>
import Wheel from '@/components/Wheel';

export default {
  components: {
    Wheel,
  },
  methods: {
    spin() {
      this.card = null;
      this.$refs.wheel.startSpin();
    },
    result(ev) {
      this.first = false;
      this.losuj = 'ZAKRĘĆ PONOWNIE';
      this.card = this.options[ev];
    }
  },
  data() {
    return {
      first: true,
      card: null,
      losuj: 'ZAKRĘĆ KOŁEM',
      options: [
        {
          name: 'maseczka antyfejkowa',
          freq: 4,
          bg: '#EC378D',
          text: '#222',
          hide: false,
          fontMod: 1.1,
          quest: 'Udostępnij w Internecie infografikę na temat koronawirusa',
          href: 'https://www.contra19.org/maseczkaantyfejkowa',
          img: 'maseczka.png',
        },
        {
          name: 'e-domóweczka',
          freq: 4,
          bg: '#D72E8A',
          text: '#222',
          hide: false,
          fontMod: 1.1,
          quest: 'Zintegruj ekipę organizując imprezę z prawdziwego zdarzenia',
          href: 'https://www.contra19.org/e-domoweczka',
          img: 'e-domoweczka.png',
        },
        {
          name: 'weź zagadaj',
          freq: 4,
          bg: '#EC378D',
          text: '#222',
          hide: false,
          fontMod: 1.1,
          quest: 'Zadzwoń do kilku osób, by nikt nie czuł się teraz samotny',
          href: 'https://www.contra19.org/wezzagadaj',
          img: 'wezzagadaj.png',
        },
        {
          name: 'przeżyj to w piżamie',
          freq: 4,
          bg: '#D72E8A',
          text: '#222',
          hide: false,
          fontMod: 1.1,
          quest: 'Obejrzyj spektakl online i wesprzyj polską kulturę',
          href: 'https://www.contra19.org/przezyjtowpizamie',
          img: 'przezyj.png',
        },
        {
          name: 'sąsiedzka sztama',
          freq: 4,
          bg: '#EC378D',
          text: '#222',
          hide: false,
          fontMod: 1.1,
          quest: 'Zrób plakat z pozytywnym przekazem i wywieś go na balkonie!',
          href: 'https://www.contra19.org/sasiedzkasztama',
          img: 'sztama.png',
        },
        {
          name: 'ugotuj coś z niczego',
          freq: 4,
          bg: '#D72E8A',
          text: '#222',
          hide: false,
          fontMod: 1.1,
          quest: 'Przetestuj swoje zdolności kulinarne i ugotuj coś dobrego!',
          href: 'https://www.contra19.org/ugotuj',
          img: 'ugotuj.png',
        },
        {
          name: 'akcja teleportacja',
          freq: 4,
          bg: '#EC378D',
          text: '#222',
          hide: false,
          fontMod: 1.1,
          quest: 'Rozmarz się i zrelaksuj wymyślając listę rzeczy do zrobienia po koronawirusie',
          href: 'https://www.contra19.org/akcjateleportacja',
          img: 'akcja.png',
        },
        {
          name: 'tańcz, nikt nie patrzy',
          freq: 4,
          bg: '#D72E8A',
          text: '#222',
          hide: false,
          fontMod: 1.1,
          quest: 'Potańcz w domu do chillowej muzyki i zadbaj o siebie!',
          href: 'https://www.contra19.org/zatanczzvibem',
          img: 'tancz.png',
        },
        {
          name: 'pokoloruj świat',
          freq: 4,
          bg: '#EC378D',
          text: '#222',
          hide: false,
          fontMod: 1.1,
          quest: 'Zostań miejskim inspiratorem i napisz motywujące sentencje',
          href: 'https://www.contra19.org/pokoloruj-swiat',
          img: 'pokoloruj.png',
        },
        {
          name: 'uratuj lato',
          freq: 4,
          bg: '#D72E8A',
          text: '#222',
          hide: false,
          fontMod: 1.1,
          quest: 'Wesprzyj panią Krysię z lokalnej lodziarni!',
          href: 'https://www.contra19.org/uratuj-lato',
          img: 'uratuj.png',
        },
      ],
      settings: {

      },
    }
  }
};
</script>
