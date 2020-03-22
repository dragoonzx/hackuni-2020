<template>
  <div class="hello">
    <div class="left-menu">
      <div class="info">
        <h2>Tracking your cargo safety</h2>
      </div>
      <div class="cargo-list">
        <vs-collapse type="shadow">
          <vs-collapse-item>
            <div slot="header" @click.capture="addMarkersAndSetViewBounds(map)">
              Cargo 1
            </div>
            Your cargo currently in trip
            <br></br>
            A: Nevskiy St. 52
            <br></br>
            B: Nevskiy St. 42
            <br></br>
            Temperature: 24
            <br></br>
            Humidity: 60
          </vs-collapse-item>
          <vs-collapse-item>
            <div slot="header">
              Cargo 2
            </div>

            Nunc auctor et leo vitae suscipit. Nullam aliquet purus scelerisque enim hendrerit tristique. Maecenas tincidunt dui arcu, a aliquet nisl venenatis vitae. Praesent mauris ligula, porta at maximus ac, rutrum vitae sapien. Donec a sapien id erat dapibus dignissim sodales in est. Donec gravida dapibus sapien at sollicitudin. Maecenas iaculis quam ex,
            <br><br>
            eu aliquam erat sagittis eget. Suspendisse mollis felis nec ipsum vehicula, at posuere libero viverra. Nam hendrerit dapibus eleifend. Aliquam elit nulla, tincidunt pellentesque enim mollis, consectetur placerat enim. Integer condimentum tristique ante et ullamcorper. Mauris placerat pretium ex. Nam aliquam sed tortor sit amet
            <br><br>
            efficitur. Mauris quis faucibus nulla. Pellentesque egestas non ipsum vel maximus.
          </vs-collapse-item>
          <vs-collapse-item disabled >
            <div slot="header">
              Cargo 3
            </div>

            Suspendisse aliquet condimentum diam, sed aliquam nisl dapibus et. Aliquam euismod ullamcorper dolor eu
          </vs-collapse-item>
          <vs-collapse-item>
            <div slot="header">
              Cargo 4
            </div>

            Suspendisse aliquet condimentum diam, sed aliquam nisl dapibus et. Aliquam euismod ullamcorper dolor eu imperdiet. Nullam eget odio at magna gravida suscipit sed vestibulum odio. Maecenas porta elit vel lectus molestie, eget aliquam enim feugiat. Vivamus nec faucibus nisl. Nunc venenatis tempus finibus.
          </vs-collapse-item>
          </vs-collapse>
      </div>
    </div>
    <div class="main-menu">
      <div ref="map" class="interactive-map" style="width: calc(100% - 30rem); height: 100vh">
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
  methods: {
    setStyle: function(map) {
        // get the vector provider from the base layer
        var provider = map.getBaseLayer().getProvider();
        // Create the style object from the YAML configuration.
        // First argument is the style path and the second is the base URL to use for
        // resolving relative URLs in the style like textures, fonts.
        // all referenced resources relative to the base path https://js.api.here.com/v3/3.1/styles/omv.
        let style = new H.map.Style('https://heremaps.github.io/maps-api-for-javascript-examples/change-style-at-load/data/dark.yaml',
          'https://js.api.here.com/v3/3.1/styles/omv/');
        // set the style on the existing layer
        provider.setStyle(style);
      },
    addMarkersAndSetViewBounds: function(map) {
      // create map objects
      // var kudrovo = new H.map.Marker({lat: 59.902692, lng: 30.512570}),
      //     boston = new H.map.Marker({lat: 55.644466, lng: 37.395744}),
      //     group = new H.map.Group();


      const marker = new H.map.Marker({lat: 59.902692, lng: 30.512570});

      var berlinMarker = new H.map.Marker({lat: 59.909623, lng: 30.312584});
      map.addObject(berlinMarker);
      

      var berlin2Marker = new H.map.Marker({lat: 59.969134, lng: 30.351177});
      map.addObject(berlin2Marker);

      const isMapAnimated = true;
      map.setCenter({lat: 59.902692, lng: 30.512570}, isMapAnimated);
      map.setZoom(11, isMapAnimated);
    }
  },
  created() {
    this.platform = new H.service.Platform({
      apikey: this.appCode
    });
  },
  mounted() {
    let maptypes = this.platform.createDefaultLayers();

    this.map = new H.Map(
        this.$refs.map,
        maptypes.vector.normal.map,
        {
            zoom: 10,
            center: { lat: 59.9342802, lng: 30.3350986 }
        }
    );

    window.addEventListener('resize', () => this.map.getViewPort().resize());

    let behavior = new H.mapevents.Behavior(new H.mapevents.MapEvents(this.map));

    // Create the default UI components
    let ui = H.ui.UI.createDefault(this.map, maptypes);
    
    this.setStyle(this.map);
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
  margin-top: 3rem;
}
.left-menu .cargo-list {
  margin-top: 4rem;
}
.vs-collapse-item--header {
  padding: 20px;
}
.main-menu {
    position: fixed;
    transition: opacity 500ms ease 0s;
    opacity: 1;
    cursor: default;
    outline: none;
    left: 30rem;
    top: 56px;
    width: 100%;
    height: 100%;
}
</style>
