<script>
  import { onMount, onDestroy } from 'svelte'
  import { Map, MapStyle, Marker, NavigationControl, config } from '@maptiler/sdk';
  import "@maptiler/sdk/dist/maptiler-sdk.css";

  let map;
  let mapContainer;

  config.apiKey = 'tZ10DN4ofU46kg5YXfJX';

  onMount(() => {
    const initialState = { lng: 121.0676, lat: 14.6503, zoom: 15 };
    const QCBounds = [
      [120.9800, 14.5900],
      [121.1350, 14.770]
    ] as const;

    map = new Map({
      container: mapContainer,
      style: "streets-v4",
      center: [initialState.lng, initialState.lat],
      zoom: initialState.zoom,
      maxBounds: QCBounds, //[
      // [120.9800, 14.5900],
      // [121.1350, 14.770]
      // ],
      pitch: 80,
      terrain: true,
      terrainExaggeration: 1.5
    });

    new Marker({color: "#FF0000"})
      .setLngLat([121.0676,14.6503])
      .addTo(map);

  });

  onDestroy(() => {
    map.remove();
  });
</script>

<div class="map-wrap">
  <div class="map" bind:this={mapContainer}></div>
</div>

<style>
  .map-wrap {
    position: relative;
    width: 100%;
    height: calc(100vh - 77px); /* calculate height of the screen minus the heading */
  }

  .map {
    position: absolute;
    width: 100%;
    height: 100%;
  }
</style>