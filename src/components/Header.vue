<template>
  <header id="solarHeader" class="solarNav">
    <div class="solarHeader_inner">
      <div class="solarContainer">
        <div class="solarRows">
          <div class="solarCol solarCol01">
            <div class="solarLogo" ref="solarLogo">
              <a href="index.htm" class="solarLogo_link">
                <span class="solarLogo_img">
                </span>
                <span class="solarLogo_text">Energy Cove</span>
              </a>
            </div>
          </div>
          <div class="solarCol solarCol02">
            <nav class="solarTopMenu" ref="solarTopMenu">
              <ul class="solarTopMenu_list">
                <li v-for="item in menuItems" :key="item.url">
                  <a :href="item.url">{{ item.text }}</a>
                </li>
              </ul>
            </nav>
            <div class="solarHeaderCTA" ref="solarGetQuote">
              <a href="#" class="solarCTA_btn solarBtn" @click.prevent="handleGetQuote">
                <div class="solarBtn_header">
                  <div class="solarLabel solarLabel1">Get Solar Quote</div>
                  <div class="solarLabel solarLabel2">Get Solar Quote</div>
                </div>
              </a>
            </div>
            <div class="solarMobileMenu">
              <button class="solarMobileMenu_btn" @click="toggleMobileMenu">
                <div class="solarMenuLines">
                  <span class="solarMenuLine solarMenuLine01"></span>
                  <span class="solarMenuLine solarMenuLine02"></span>
                </div>
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </header>
</template>

<script>
import { ref, onMounted } from 'vue'
import gsap from 'gsap'

export default {
  name: 'SolarHeader',
  setup() {
    const solarLogo = ref(null)
    const solarTopMenu = ref(null)
    const solarGetQuote = ref(null)

    const menuItems = ref([
      { url: 'about/index.html', text: 'About Us' },
      { url: 'services/index.htm', text: 'Solar Solutions' },
      { url: 'products/index.htm', text: 'Solar Products' },
      { url: 'portfolio/index.htm', text: 'Project Portfolio' },
      { url: 'contacts/index.htm', text: 'Contact' },
    ])

    const handleGetQuote = () => {
      console.log('Get a solar quote clicked')
    }

    const toggleMobileMenu = () => {
      console.log('Solar mobile menu toggled')
    }

    onMounted(() => {
      // setTimeout(() => {
      //
      // }, 100)

      // Initial state
      gsap.set([solarLogo.value, solarTopMenu.value], {
        y: '-7.813vw',
        opacity: 0
      })
      gsap.set(solarGetQuote.value, {
        x: '18.229vw',
        opacity: 0
      })

      // Animation timeline
      const tl = gsap.timeline({ defaults: { ease: 'power3.out' } })

      tl.to([solarLogo.value, solarTopMenu.value], {
        y: 0,
        opacity: 1,
        duration: 1,
        stagger: 0.2
      })
          .to(solarGetQuote.value, {
            x: 0,
            opacity: 1,
            duration: 1
          }, '-=0.5')
    })

    return {
      menuItems,
      handleGetQuote,
      toggleMobileMenu,
      solarLogo,
      solarTopMenu,
      solarGetQuote
    }
  }
}
</script>

<style>
.solarNav {
  color: #0d0d0d;
}
.solarLogo_text {
  color: #000;
}

@media (min-width: 320px){
  body {
    background: transparent;
    line-height:1;
    font-family:SuisseIntl;
    font-size:62.5%;
  }
}
@media (min-width: 320px){
  * {
    outline: 0;
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }

  body {
    margin: 0;
  }

  body {
    line-height: 1;
    font-family: SuisseIntl;
  }

  body {
    overflow: hidden;
  }

  html {
    line-height: 1.15;
    -webkit-text-size-adjust: 100%;
  }

  html {
    line-height: 1;
    font-family: SuisseIntl;
  }

  html {
    font-size: 62.5%;
  }

  .solarContainer {
    max-width: 100%;
    width: 100%;
    margin-left: auto;
    margin-right: auto;
    padding: 0 2.917vw;
  }

  .solarContainer  {
    position: relative;
  }

  *,:after,:before {
    outline: 0;
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }

  .solarRows  {
    display: flex;
    justify-content: space-between;
    align-items: flex-start;
    padding-top: 1.719vw;
  }

  .solarRows .solarCol.solarCol02  {
    display: flex;
  }

  .solarRows .solarLogo  {
    opacity: 0;
    transform: translateY(-7.813vw);
    margin: 0;
    mix-blend-mode: difference;
  }

  .solarRows .solarTopMenu  {
    opacity: 0;
    transform: translateY(-7.813vw);
    margin: -.313vw 19.01vw 0 0;
  }

  .solarRows .solarHeaderCTA  {
    opacity: 1;
    transform: translatex(18.229vw);
    position: absolute;
    top: 0;
    right: 0;
  }

  .solarRows .solarMobileMenu  {
    margin: 0;
    display: none;
    margin-top: 3px;
  }

  a {
    text-decoration: none;
  }

  a {
    background-color: transparent;
  }

  .solarRows .solarLogo .solarLogo_link  {
    display: flex;
  }

  a:hover {
    text-decoration: none;
    outline: 0;
  }

  ul {
    list-style: none;
    margin: 0;
    padding: 0;
  }

  .solarRows .solarTopMenu .solarTopMenu_list  {
    display: flex;
  }

  .solarRows .solarHeaderCTA .solarCTA_btn  {
    background: #151919;
    display: inline-block;
    padding: 1.406vw 7.917vw 1.406vw 1.302vw;
    border-radius: 0 0 0 .521vw;
    color: #fff;
    font: normal .833vw/.833vw Atyp;
    letter-spacing: -.008vw;
    position: relative;
  }

  .solarNav .solarRows .solarHeaderCTA .solarCTA_btn::after {
    content: "";
    position: absolute;
    top: 0;
    bottom: 0;
    margin: auto;
    right: 1.563vw;
    width: 1.458vw;
    height: .573vw;
  }

  button {
    font-family: inherit;
    font-size: 100%;
    line-height: 1.15;
    margin: 0;
  }

  button {
    overflow: visible;
  }

  button {
    text-transform: none;
  }

  button {
    -webkit-appearance: button;
  }

  .solarRows .solarMobileMenu .solarMobileMenu_btn  {
    background: transparent;
    border: 0;
    display: flex;
    justify-content: space-between;
    align-items: center;
    cursor: pointer;
  }

  .solarRows .solarLogo .solarLogo_link .solarLogo_text  {
    display: block;
    width: 4.948vw;
    color: #000;
    font: normal .729vw/.729vw Atyp;
    margin: -.208vw 0 0 .781vw;
    letter-spacing: .013vw;
    transition: .45s;
  }

  ul li  {
    vertical-align: top;
  }

  .solarRows .solarTopMenu .solarTopMenu_list li  {
    margin: 0 2.135vw 0 0;
  }

  .solarRows .solarTopMenu .solarTopMenu_list li:last-child  {
    margin-right: 0;
  }

  .solarBtn_header {
    overflow: hidden;
    position: relative;
  }

  .solarRows .solarHeaderCTA .solarCTA_btn .solarBtn_header  {
    overflow: hidden;
    position: relative;
  }

  .solarRows .solarMobileMenu .solarMobileMenu_btn .solarMenuLines  {
    width: 48px;
    height: 8px;
    position: relative;
  }

  img {
    vertical-align: middle;
    border: 0;
    -ms-interpolation-mode: bicubic;
    height: auto;
    max-width: 100%;
  }

  img {
    border-style: none;
  }

  .solarRows .solarLogo .solarLogo_link img  {
    width: 1.823vw;
  }

  .solarRows .solarTopMenu .solarTopMenu_list li a  {
    color: #000;
    font: normal .833vw/.833vw Atyp;
    letter-spacing: -.008vw;
    transition: .4s;
  }
}

@media (min-width: 769px){
  .solarNav .solarRows .solarTopMenu .solarTopMenu_list li a:hover {
    transition: .4s;
    color: #0047ab;
    opacity: 1;
    text-shadow: none;
  }
}

@media (min-width: 320px){
  .solarBtn_header .solarLabel  {
    display: block;
  }

  .solarBtn_header .solarLabel.solarLabel1  {
    position: absolute;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
  }

  .solarRows .solarHeaderCTA .solarCTA_btn .solarBtn_header .solarLabel  {
    line-height: .99vw;
    display: block;
  }

  .solarRows .solarHeaderCTA .solarCTA_btn .solarBtn_header .solarLabel.solarLabel1  {
    position: absolute;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
  }

  .solarRows .solarMobileMenu .solarMobileMenu_btn .solarMenuLines .solarMenuLine  {
    display: block;
    background: #000;
    height: 2px;
    margin: 0;
    width: 100%;
    will-change: transform;
    transition: .45s;
    box-shadow: 0 0 2px rgba(0,0,0,0.5);
  }

  .solarRows .solarMobileMenu .solarMobileMenu_btn .solarMenuLines .solarMenuLine.solarMenuLine02  {
    margin-top: 4px;
    width: 36px;
    margin-left: auto;
  }

  .solarBtn_header .word  {
    display: inline-block;
  }

  .solarRows .solarHeaderCTA .solarCTA_btn .solarBtn_header .word  {
    display: inline-block;
  }

  .solarBtn_header .word .char  {
    display: inline-block;
  }

  .solarRows .solarHeaderCTA .solarCTA_btn .solarBtn_header .word .char  {
    display: inline-block;
  }

  .solarBtn_header .solarLabel.solarLabel2 .word .char  {
    transform: translateY(100%);
  }

  .solarRows .solarHeaderCTA .solarCTA_btn .solarBtn_header .solarLabel.solarLabel2 .word .char  {
    transform: translateY(100%);
  }
}
</style>