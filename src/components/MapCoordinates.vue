<template>
    <div>
        <h3>Map Coordinates: </h3>
        <p>Latitude: {{ lat }}</p>
        <p>Longitude: {{ lng }}</p>
    </div>
</template>

<script>
export default {
    name:'MapCoordinates',
    props:['lat', 'lng']
}
</script>