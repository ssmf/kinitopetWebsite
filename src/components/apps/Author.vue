<script setup></script>

<template>
  <div class="Author col">
    <h1>TROY_EN</h1>
    <h3>
      █ │█│ ███ █│██ │ █│ <br />
      █ │█│ ███ █│██ │ █│ <br />
      █ │█│ ███ █│██ │ █│ <br />
      █ │█│ ███ █│██ │ █│ <br />
    </h3>

    <div class="LinksWrapper col">
      <h2>You can find Troy_en here:</h2>
      <div class="Links col">
        <h4 class="Twitter">
          Twitter:
          <a href="https://twitter.com/troy_en" target="_blank">https://twitter.com/troy_en</a>
        </h4>
        <h4 class="Patreon">
          Patreon:
          <a href="https://www.patreon.com/troy_en" target="_blank"
            >https://www.patreon.com/troy_en</a
          >
        </h4>
        <h4 class="Discord">
          Discord:
          <a href="https://discord.gg/kinitopet" target="_blank">https://discord.gg/kinitopet</a>
        </h4>
        <h4 class="Spotify">
          Spotify:
          <a href="https://open.spotify.com/artist/7ywjWmkPfDKg9WvUXLPkhe" target="_blank"
            >https://open.spotify.com/artist/7ywjWmkPfDKg9WvUXLPkhe</a
          >
        </h4>
        <h4 class="Youtube">
          Youtube:
          <a href="https://www.youtube.com/@troy_en" target="_blank"
            >https://www.youtube.com/@troy_en</a
          >
        </h4>
        <h4 class="Email">
          Email:
          <a href="mailto:troyenemail@gmail.com" target="_blank">troyenemail@gmail.com</a>
        </h4>
        <h4 class="PersonalWebsite">
          Personal Website:
          <a href="https://l-l.dev/" target="_blank">https://l-l.dev/</a>
        </h4>
      </div>
    </div>
  </div>
</template>

<style scoped>
.Twitter::before,
.Patreon::before,
.Discord::before,
.Spotify::before,
.Youtube::before,
.Email::before,
.PersonalWebsite::before {
  content: ' ';
  min-height: 28px;
  min-width: 28px;
  display: inline-block;
  position: relative;
  top: 6px;
  background-image: url('/public/Media/Twitter.webp');
  background-size: cover;
}

.Patreon::before {
  background-image: url('/public/Media/Patreon.webp');
}

.Discord::before {
  background-image: url('/public/Media/Discord.webp');
}

.Spotify::before {
  background-image: url('/public/Media/Spotify.webp');
}

.Youtube::before {
  background-image: url('/public/Media/Youtube.gif');
}

.Email::before {
  background-image: url('/public/Media/Email.gif');
}

.PersonalWebsite::before {
  background-image: url('/public/Media/Globe.gif');
}

a,
h4 {
  display: inline-block;
  position: relative;
  font-size: var(--linkSize);
}

a,
a:visited {
  color: var(--darkBlue);
}

a:hover {
  color: var(--seaColor);
  background-color: rgba(0, 0, 0, 0);
}

a:active {
  top: 2px;
  left: 2px;
}

h1 {
  font-size: var(--windowHeaderSize);
}

h3 {
  font-size: var(--windowSecondHeaderSize);
  line-height: 1.1rem;
  letter-spacing: 0.2rem;
}

.Author {
  gap: 10px;
  width: 600px;
}

.LinksWrapper {
  width: 100%;
}

.Links {
  width: 100%;
  align-items: flex-start;
}
</style>
