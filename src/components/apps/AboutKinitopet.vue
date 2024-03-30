<script setup>
const redirect = () => {
  window.open('https://store.steampowered.com/app/2075070/KinitoPET/', '_blank')
}
</script>

<template>
  <div class="AboutKinitopet col">
    <div class="Header col">
      <h2>KinitoPet - Your <span class="pinkBackground">new BEST friend!</span></h2>
      <div class="HeaderGifs row">
        <img src="/public/Media/Star.gif" class="SmallGif" />
        <video
          src="/public/Media/AboutKinitopetHQ.webm"
          autoplay
          loop
          muted
          class="GameDiscGif"
        ></video>
        <img src="/public/Media/Star.gif" class="SmallGif" />
      </div>
      <h3>
        KinitoPET invites you to their <span class="orange">wonderful</span> world, full of fun and
        excitement! <br />There, he will be your very own virtual
        <span class="seaBlue">friend</span> and personal helper!
      </h3>
    </div>
    <div class="sectionBreak"></div>
    <div class="HeaderDescription">
      <p>
        <span class="pink">Kinito</span> is able to walk, talk, browse, adapt, and play games; as
        Kinito is like no other with its <span class="seaBlue">adaptive technology!</span>
      </p>
      <p>
        <span class="pink">Kinito</span> is a friend you'll never forget with its critically
        acclaimed <span class="darkBlue">R.R.A</span> to make your experience truly unique.
      </p>
      <p>
        where else can you find a friend like Kinito with its multitude of great features and
        friendly <span class="red love">love!</span>
      </p>
    </div>
    <div class="sectionBreak"></div>
    <div class="KinitoDescription col">
      <div class="col">
        <h2 class="KinitoTitle">Meet <span class="pink">Kinito!</span></h2>
        <h4>
          <span class="pink">Kinito</span> is a friendly, fun-loving companion who can keep your
          computer <span class="green">safe!</span> <br /><span class="gray"
            >(NOTE: KinitoPET might not keep your computer safe).</span
          ><br />
          His multitude of great <span class="seaBlue">features</span> go hand in hand with his
          upstanding personality that is sure to keep you
          <span class="underline">entertained!</span>
        </h4>
      </div>
      <div class="row">
        <div class="col" style="gap: 15px; margin-bottom: 60px">
          <p>
            Kinito has always been the face of the 1986's Kinito
            <span class="orange">Crew collection</span> and that is why we are delighted to bring
            our loveable mascot into the <span class="darkBlue">digital</span> age!
          </p>
          <p>So why wait? Add <span class="pink">KinitoPET</span> to your machine today!</p>
        </div>
        <img src="/public/Media/KinitoSurfboard.webp" style="margin: 0px -40px; scale: 1.2" />
      </div>
      <div class="col" style="margin-top: -80px">
        <p class="BookIcon">
          "I can read!" - Kinito will <span class="darkBlue">WOW</span> you with his heartfelt
          stories!
        </p>
        <p class="MonitorIcon">
          "I play games!" - The KinitoPET virtual assistant comes with a multitude of online games
          from the likes of the beloved <span class="seaBlue">Kinito Crew!</span>
        </p>
        <p class="SpiralIcon">
          "I adapt to you!" - Form a <span class="red">deep</span> connection with
          <span class="pink">KinitoPET</span> as with the top of the line
          <span class="darkBlue">R.R.A</span> technology, KinitoPET is able to give randomised
          conversations based on <span class="green">REAL</span> WORLD EXAMPLES!
        </p>
      </div>
    </div>
    <div class="sectionBreak"></div>
    <div class="WebWorldSection col">
      <div class="row">
        <img src="/public/Media/WebWorld.webp" style="width: 50%; rotate: -20deg" />
        <div class="col" style="rotate: 15deg">
          <img class="BigIcon" src="/public/Media/Clover.gif" style="margin-bottom: -15px" />
          <div class="row">
            <img class="BigIcon" src="/public/Media/Star3D.gif" alt="3d rotating star" />
            <h2 class="WebWorldHeading">
              Welcome To The <br /><span class="darkBlue">Web</span>
              <span class="green">World!</span>
            </h2>
            <img class="BigIcon" src="/public/Media/Star3D.gif" alt="3d rotating star" />
          </div>
          <img class="BigIcon" src="/public/Media/Globe.gif" />
        </div>
      </div>
      <div class="TextSection col">
        <p>
          <span class="pink">KinitoPET</span> comes packaged with The
          <span class="seaBlue">Kinito Crews</span> <span class="darkBlue">Web </span>
          <span class="green">World</span> a fun and entertaining place where you can meet the
          beloved Kinito Crew characters in a new <span class="darkBlue">digital</span> form.
        </p>
        <p>
          <span class="green">Jade</span> the Jellyfish, <span class="pink">Kinito</span> the
          Axolotl and <span class="orange">Sam</span> the Sea Anemone meet once again through small
          games and puzzles that will keep you entertained!
        </p>
        <p>
          Learn new <span class="seaBlue">fun</span> facts about the ocean of our planet with
          amazing games suited <span class="underline">just for you!</span>
        </p>
      </div>
    </div>
    <div class="sectionBreak"></div>
    <div class="GetKinitopetSection col">
      <h2 class="GetKinitopetCopy">
        So why wait! Get your new <span class="pink">best friend</span> companion for just
        <span class="green">5.99$</span> <span class="red">!!!</span>
      </h2>
      <button class="BuyKinitopetButton" @click="redirect">GET KINITOPET</button>
    </div>
  </div>
</template>

<style scoped>
* {
  text-align: center;
}

.AboutKinitopet {
  width: 950px;
  height: 700px;
  overflow: auto;
  padding: 15px;
  gap: 20px;
  overflow-x: hidden;
}

.GetKinitopetSection {
  gap: 20px;
}

.BuyKinitopetButton {
  font-size: var(--windowSecondHeaderSize);
  background-color: var(--pink);
  padding: 10px 20px;
  border: 3px solid black;
  box-shadow: 3px 3px 0px 3px var(--gray);
  rotate: 0deg;
  transition: 1s all ease-in-out;
}

.BuyKinitopetButton:hover {
  rotate: 360deg;
  cursor: pointer;
}

p {
  font-size: var(--windowTextSize);
}

h2 {
  font-size: var(--windowHeaderSize);
}

h3 {
  font-size: var(--windowSecondHeaderSize);
}

h4 {
  font-size: var(--windowThirdHeaderSize);
}

.pinkBackground {
  background-color: var(--pink);
}

.col {
  justify-content: flex-start;
}

.row {
  display: flex;
  align-items: center;
  justify-content: center;
}

.GameDiscGif {
  width: 70%;
}

.SmallGif {
  height: 40px;
}

.sectionBreak {
  display: inline-block;
  width: 100%;
  min-height: 10px;
  background-image: url('/public/Media/SectionBreak.webp');
}

.KinitoDescription {
  gap: 40px;
  width: 90%;
}

.WebWorldSection {
  margin-top: 100px;
}

.BigIcon {
  width: 70px;
}

.WebWorldHeading {
  font-size: 50px;
  line-height: 45px;
  padding: 20px 0px;
  width: max-content;
}

.TextSection {
  margin-top: 90px;
  gap: 15px;
}

.love::before,
.love::after,
.KinitoTitle::before,
.KinitoTitle::after,
.BookIcon::before,
.MonitorIcon::before,
.SpiralIcon::before,
.GetKinitopetCopy::before {
  display: inline-block;
  content: ' ';
  position: relative;
  top: 5px;
  background-size: contain;
  background-image: url('/public/Media/Heart.gif');
  min-height: 32px;
  min-width: 32px;
}

.GetKinitopetCopy::before {
  background-image: url('/public/Media/BuyTheGame.gif');
  min-height: 40px;
  min-width: 40px;
  background-size: cover;
}

.BookIcon::before {
  background-image: url('/public/Media/Book.gif');
}

.MonitorIcon::before {
  background-image: url('/public/Media/Monitor.gif');
}

.SpiralIcon::before {
  background-image: url('/public/Media/PinkSpiral.gif');
}

.KinitoTitle::before {
  background-image: url('/public/Media/Sparkle1.gif');
  rotate: 20deg;
  left: 6px;
}

.KinitoTitle::after {
  background-image: url('/public/Media/Sparkle2.gif');
  rotate: -30deg;
}
</style>
