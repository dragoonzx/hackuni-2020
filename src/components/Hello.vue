<template>
  <div class="hello">
    <div class="left-menu">
      <div class="info">
        <h2>Tracking your cargo safety</h2>
        <p>Bla bla bla</p>
      </div>
      <div class="cargo-list">

      </div>
    </div>
    <div class="main-menu">
      <div ref="map" id="mapContainer" class="interactive-map" style="width: 400px; height: 400px">
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'hello',
  data() {
    return {
      msg: 'Welcome to Your Vue.js PWA',
      map: {},
      platform: {},
      appId: 'dWuK9yGmEm8ukYeHW5f4',
      appCode: 'hrieRalCaIPMe1vXiZTw6_Amyfi2VVomjBvOLmz1lOs'
    };
  },
  created() {
    this.platform = new H.service.Platform({
      'apikey': this.appCode
    });
  },
  mounted() {
    this.map = new H.Map(
        document.getElementById('mapContainer'),
        this.platform.createDefaultLayers().normal.map,
        {
            zoom: 10,
            center: { lat: 52.5, lng: 13.4 }
        }
    );
}
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #35495E;
}

.left-menu {
  position: fixed;
  top: 56px;
  left: 0;
  bottom: 0;
  z-index: 999999;
  border-top: 0.25rem solid #00AFAA;
  width: 30rem;
  box-shadow: 0 10px 15px -3px rgba(0,0,0,0.1), 0 4px 6px -2px rgba(0,0,0,0.05);
  overflow: scroll;
  background-color: #fff;
  padding-bottom: 5rem;
}
.left-menu .info {
  padding-left: 1.25rem;
  padding-right: 1.25rem;
  padding-top: 1.25rem;
}
.main-menu {
    position: fixed;
    transition: opacity 500ms ease 0s;
    opacity: 1;
    cursor: default;
    outline: none;
    left: 30rem;
}
</style>
