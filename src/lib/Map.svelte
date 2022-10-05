<script>
  import { Map as LeafletMap, Icon, Marker } from "leaflet";
  import { FeatureLayer } from "esri-leaflet";
  import { vectorBasemapLayer } from "esri-leaflet-vector";

  import "leaflet/dist/leaflet.css";

  import icon from "leaflet/dist/images/marker-icon.png";
  import iconShadow from "leaflet/dist/images/marker-shadow.png";

  // This variable gets replaced by vite -
  // see https://vitejs.dev/guide/env-and-mode.html
  const apiKey = import.meta.env.VITE_ARCGIS_API_KEY;

  const map = (domNode) => {
    let DefaultIcon = new Icon({
      iconUrl: icon,
      shadowUrl: iconShadow,
      iconAnchor: [12, 41],
      popupAnchor: [0, -41],
    });
    Marker.prototype.options.icon = DefaultIcon;

    const map = new LeafletMap(domNode);
    map.setView([25.773924, -80.196075], 6);

    vectorBasemapLayer("ArcGIS:Streets", {
      apiKey, // https://developers.arcgis.com
    }).addTo(map);

    // Add a Feature Layer
    const fl = new FeatureLayer({
      url: "https://sampleserver6.arcgisonline.com/arcgis/rest/services/SampleWorldCities/MapServer/0",
    }).addTo(map);

    fl.bindPopup(function (layer) {
      return `<p><strong>${
        layer.feature.properties.CITY_NAME
      }</strong><br /> Population: ${layer.feature.properties.POP.toLocaleString("en")}</p>`;
    });
  };
</script>

<div use:map />

<style>
  div {
    height: 100%;
    width: 100%;
  }
</style>