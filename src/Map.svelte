<script>
  import { Map as LeafletMap, Icon, Marker } from "leaflet";
  import { VERSION, BasemapLayer, FeatureLayer } from "esri-leaflet";
  import "leaflet/dist/leaflet.css";

  const map = (domNode) => {
    const map = new LeafletMap(domNode);
    map.setView([53.35014, -6.266155], 8);

    const basemap = new BasemapLayer("Streets");
    map.addLayer(basemap);
  };
</script>

<div use:map />

<style>
  div {
    height: 100%;
    width: 100%;
  }
</style>
