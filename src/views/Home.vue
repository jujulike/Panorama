<template>
  <div id="home">
  </div>
</template>

<script>
import PhotoShereViewer from "photo-sphere-viewer";

export default {
  name: "home",
  data() {
    return {};
  },
  created() {
    this.$nextTick(() => {
      this._photoShereViewer();
    });
  },
  methods: {
    _photoShereViewer() {
      let psv = new PhotoShereViewer({
        panorama: "/img/test.jpg",
        container: "home",
        markers: [
          {
            id: "image",
            longitude: 0,
            latitude: 0,
            image: "/img/pin1.png",
            width: 32,
            height: 32
          }
        ]
      });
      // 添加标记
      psv.on("click", function(e) {
        psv.addMarker({
          id: `#${Math.random()}`,
          longitude: e.longitude,
          latitude: e.latitude,
          image: "/img/pin1.png",
          width: 32,
          height: 32
        });
      });
      psv.on("select-marker", function(marker) {
        psv.gotoMarker(marker, 1000).then(() => {
          setInterval(() => {
            marker.longitude += 0.001;
            marker.latitude += 0.001;
            psv.updateMarker(marker, true);
            psv.gotoMarker(marker);
          }, 20)
        });
      });
    }
  }
};
</script>
<style lang="stylus" scoped>
#home {
  position: absolute;
  top: 0;
  right: 0;
  left: 0;
  bottom: 0;
}
</style>

