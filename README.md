<html>
<head>
<meta charset="utf-8" />
<title>Add a geocoder</title>
<meta name="viewport" content="initial-scale=1,maximum-scale=1,user-scalable=no" />
<script src="https://api.mapbox.com/mapbox-gl-js/v1.9.0/mapbox-gl.js"></script>
<link href="https://api.mapbox.com/mapbox-gl-js/v1.9.0/mapbox-gl.css" rel="stylesheet" />
<style>
	body { margin: 0; padding: 0; }
	#map { position: absolute; top: 0; bottom: 0; width: 100%; }
</style>
</head>
<body>
<script src="https://api.mapbox.com/mapbox-gl-js/plugins/mapbox-gl-geocoder/v4.4.2/mapbox-gl-geocoder.min.js"></script>
<link
    rel="stylesheet"
    href="https://api.mapbox.com/mapbox-gl-js/plugins/mapbox-gl-geocoder/v4.4.2/mapbox-gl-geocoder.css"
    type="text/css"
/>
<!-- Promise polyfill script required to use Mapbox GL Geocoder in IE 11 -->
<script src="https://cdn.jsdelivr.net/npm/es6-promise@4/dist/es6-promise.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/es6-promise@4/dist/es6-promise.auto.min.js"></script>
<div id="map"></div>
<script>
	mapboxgl.accessToken = 'pk.eyJ1IjoiYmFsbGVyZWF1IiwiYSI6ImNrOGZ5Z3M2MzA0dHAzZXBrcDQwbzN5YzIifQ.UpKvOA9C3E4M9bOoG7r1yg';
    var map = new mapboxgl.Map({
        container: 'map',
        style: 'mapbox://styles/ballereau/ck7bzhy7q00fq1irwkzovmv89',
        center: [2.306518, 48.523618],
        zoom: 8.3
    });
    map.addControl(
        new MapboxGeocoder({
            accessToken: mapboxgl.accessToken,
   // limit results to France
    countries: 'fr',
            mapboxgl: mapboxgl
        })
    );
    map.on('click', function(e) {
  var features = map.queryRenderedFeatures(e.point, {
    layers: ['prises-commercialisables'] // replace this with the name of the layer
  });
  if (!features.length) {
    return;
  }
  var feature = features[0];
  var popup = new mapboxgl.Popup({
      offset: [0, -15]
    })
    .setLngLat(feature.geometry.coordinates)
    .setHTML("Bâtiment éligible : " +'</p>' + feature.properties.Voie +'</p>'+feature.properties.Commune +'</p>'+ "Date d'ouverture d'éligibilité :" + feature.properties.DateOuvertureEligibilite +'</p>'+"ad_hexaclé :" + feature.properties.ad_hexacle + '</p>' + "ad_batcode :" + feature.properties.ad_batcode + '</p>')
    .addTo(map);
});
// Change the cursor to a pointer when the mouse is over the prises-commercialisables layer.
map.on('mouseenter', 'prises-commercialisables', function() {
map.getCanvas().style.cursor = 'pointer';
});
// Change it back to a pointer when it leaves.
map.on('mouseleave', 'prises-commercialisables', function() {
map.getCanvas().style.cursor = '';
});

    map.on('click', function(e) {
  var features = map.queryRenderedFeatures(e.point, {
    layers: ['prises-arcep'] // replace this with the name of the layer
  });
  if (!features.length) {
    return;
  }
  var feature = features[0];
  var popup = new mapboxgl.Popup({
      offset: [0, -15]
    })
    .setLngLat(feature.geometry.coordinates)
    .setHTML("Bâtiment éligible : " +'</p>' + feature.properties.Voie +'</p>'+feature.properties.Commune +'</p>' + "ad_hexaclé : " + feature.properties.imb_id +'</p>' + "État : déployé ")
    .addTo(map);
});
// Change the cursor to a pointer when the mouse is over the prises-arcep layer.
map.on('mouseenter', 'prises-arcep', function() {
map.getCanvas().style.cursor = 'pointer';
});
// Change it back to a pointer when it leaves.
map.on('mouseleave', 'prises-arcep', function() {
map.getCanvas().style.cursor = '';
});


map.on('load', function() {
// Add a source for the JALON polygons.
map.addSource('Jalon4', {
'type': 'geojson',
'data':
'ballereau.13ncrgcs'
});
 
 
// When a click event occurs on a feature in the states layer, open a popup at the
// location of the click, with description HTML from its properties.
map.on('click', 'Jalon4', function(e) {
new mapboxgl.Popup()
.setLngLat(e.lngLat)
.setHTML('<strong>Jalon 4</strong>' +'</p>'+ "Nom de la zone : " + e.features[0].properties.zs_r3_code +'</p>' + "Date d'ouverture commerciale : " + e.features[0].properties.DATE_OUVERTURE)
.addTo(map);
});
 
// Change the cursor to a pointer when the mouse is over the JALON layer.
map.on('mouseenter', 'Jalon4', function() {
map.getCanvas().style.cursor = 'pointer';
});
 
// Change it back to a pointer when it leaves.
map.on('mouseleave', 'Jalon4', function() {
map.getCanvas().style.cursor = '';
});
});

map.on('load', function() {
// Add a source for the JALON polygons.
map.addSource('Jalon3', {
'type': 'geojson',
'data':
'ballereau.1yt4fw1z'
});
 
 
// When a click event occurs on a feature in the states layer, open a popup at the
// location of the click, with description HTML from its properties.
map.on('click', 'Jalon3', function(e) {
new mapboxgl.Popup()
.setLngLat(e.lngLat)
.setHTML('<strong>Jalon 3</strong>' +'</p>'+ "Nom de la zone : " + e.features[0].properties.zs_r3_code +'</p>' + "Date d'ouverture commerciale : " + e.features[0].properties.DATE_OUVERTURE)
.addTo(map);
});
 
// Change the cursor to a pointer when the mouse is over the JALON layer.
map.on('mouseenter', 'Jalon3', function() {
map.getCanvas().style.cursor = 'pointer';
});
 
// Change it back to a pointer when it leaves.
map.on('mouseleave', 'Jalon3', function() {
map.getCanvas().style.cursor = '';
});
});

map.on('load', function() {
// Add a source for the JALON polygons.
map.addSource('Jalon2', {
'type': 'geojson',
'data':
'ballereau.0jrde1xu'
});
 
 
// When a click event occurs on a feature in the JALON layer, open a popup at the
// location of the click, with description HTML from its properties.
map.on('click', 'Jalon2', function(e) {
new mapboxgl.Popup()
.setLngLat(e.lngLat)
.setHTML('<strong>Jalon 2</strong>' +'</p>'+ "Nom de la zone : " + e.features[0].properties.zs_r3_code +'</p>' + "Date d'ouverture commerciale : " + e.features[0].properties.DATE_OUVERTURE)
.addTo(map);
});
 
// Change the cursor to a pointer when the mouse is over the JALON layer.
map.on('mouseenter', 'Jalon2', function() {
map.getCanvas().style.cursor = 'pointer';
});
 
// Change it back to a pointer when it leaves.
map.on('mouseleave', 'Jalon2', function() {
map.getCanvas().style.cursor = '';
});
});

map.on('load', function() {
// Add a source for the JALON polygons.
map.addSource('Jalon1', {
'type': 'geojson',
'data':
'ballereau.9oqswgyq'
});
 
 
// When a click event occurs on a feature in the JALON layer, open a popup at the
// location of the click, with description HTML from its properties.
map.on('click', 'Jalon1', function(e) {
new mapboxgl.Popup()
.setLngLat(e.lngLat)
.setHTML('<strong>Jalon 1</strong>' +'</p>'+ "Nom de la zone : " + e.features[0].properties.zs_r3_code +'</p>' + "Date d'ouverture commerciale : " + e.features[0].properties.DATE_OUVERTURE)
.addTo(map);
});
 
// Change the cursor to a pointer when the mouse is over the JALON layer.
map.on('mouseenter', 'Jalon1', function() {
map.getCanvas().style.cursor = 'pointer';
});
 
// Change it back to a pointer when it leaves.
map.on('mouseleave', 'Jalon1', function() {
map.getCanvas().style.cursor = '';
});
});
</script>
