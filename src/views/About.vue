<template>
  <div id="about">
    <p class="icon">🏞</p>
    <h1>Parks Wiki <span>(WINNIPEG)</span></h1>
    <p class="info">
      This is a version 2 of my old project created as assigment during college.
      The app fetches all parks and open spaces in Winnipeg city from
      <b>Winnipeg Data API</b> and shows them on the map.
      checkout my old project
      <a href="https://winnipeg-parks-wiki.now.sh/" target="_blank" color="black">here</a>.
      <br><br><br>
      Thank you for visiting my website 🙏!
    </p>
  </div>
</template>

<style lang="scss" scoped>
#about {
  min-height: 100vh;
  height: 100%;
  width: 100%;
  text-align: center;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
}

h1 {
  span {
    opacity: 0.5;
    font-size: 18px;
  }
}

.icon {
  font-size: 100px;
  margin-bottom: 0;
}

.info {
  max-width: 500px;
  font-size: 18px;
  margin-top: 16px;
  opacity: 0.8;
}
</style>
