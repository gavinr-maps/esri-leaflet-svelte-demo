<script>
  import { Map as LeafletMap, Icon, Marker } from "leaflet";
  // import { VERSION, BasemapLayer, FeatureLayer } from "esri-leaflet";
  import { vectorBasemapLayer } from "esri-leaflet-vector";

  import "leaflet/dist/leaflet.css";

  const map = (domNode) => {
    const map = new LeafletMap(domNode);
    map.setView([53.35014, -6.266155], 8);

    vectorBasemapLayer("ArcGIS:Streets", {
      apiKey: "< YOUR VALID API KEY HERE >", // https://developers.arcgis.com
    }).addTo(map);
  };
</script>

<div use:map />

<style>
  div {
    height: 100%;
    width: 100%;
  }
</style>
