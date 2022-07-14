<template>
  <!-- Prop title anzeigen -->
  <h1>{{ title }}</h1>
  <ul class="list">
    <!-- Anstatt <li> können auch andere HTML-Elemente verwendet werden -->
    <li v-for="(item, index) in items" :key="index">
      <button @click="onClickCheckbox(index)">delete</button>
      <!-- Dynammische CSS Klasse -->
      <span><span id="NameSpan">{{ item.name + ":"}}</span>{{" ca. " + calculateDistance(point, item.coordinates) + " m"}}</span>
    </li>
  </ul>
</template>

<script>
export default {
  name: "MyList",
  // Props oder Properties können aus App.vue übergeben werden.
  props: {
    title: String,
  },
  // Die Daten für die Komponente
  data: function () {
    return {
      newItemText: "",
      items: [
        { coordinates: [6.9570, 50.9367], name: "Köln" },
        { coordinates: [4.9041, 52.3676], name: "Amsterdam" },
        { coordinates: [9.4797, 51.3127], name: "Kassel" },
        { coordinates: [2.1686, 41.3874], name: "Barcelona" },
        { coordinates: [10.1815, 36.8065], name: "Tunis" },
        { coordinates: [135.7681,35.0116], name: "Kyoto" },
        { coordinates: [26.1025, 44.4268], name: "Bucharest" },
        { coordinates: [15.4395, 47.0707], name: "Graz" },
        { coordinates: [31.2357, 30.0444], name: "Kairo" },
        { coordinates: [6.2603, 53.3498], name: "Dublin" },
        { coordinates: [10.7522, 59.9139], name: "Oslo" }
      ],
      point: [7.595737,51.969508],
      hover: false,
    };
  },
  // Funktionen für die Komponenten.
  // Können aus <template> aufgerufen werden oder
  // aus anderen Methoden mit this.myCustomMethod();
  methods: {
    /**
     * Element aus der Liste als erledigt oder nicht erledigt markieren.
     * @param {number} index
     */
    onClickCheckbox(index) {
      this.items.splice(index, 1,);
    },
    /**
     * Calculates the distances between two Arrays of coordinates
     * @param {array} firstArray
     * @param {array} secondArray
     */
    calculateDistance(point, city){
      let R = 6371e3; // mean radius of the earth
      const lat1 = point[1] * Math.PI/180; // is constant because we only compare with one point
      let lat2 = city[1] * Math.PI/180; 
      let latRechner = (city[1] - point[1]) * Math.PI/180;
      let lonRechner = (city[0] - point[0]) * Math.PI/180;

      let a = Math.sin(latRechner/2) * Math.sin(latRechner/2) +
            Math.cos(lat1) * Math.cos(lat2) *
            Math.sin(lonRechner/2) * Math.sin(lonRechner/2);
      let c = 2 * Math.atan2(Math.sqrt(a), Math.sqrt(1-a));

      let d = R * c;
      return Math.round(d); // returns the distance in metres
    }
  },
};
</script>

<style scoped>
.list {
  display: flex;
  flex-direction: column;
  align-items: center;
  list-style-type: none;
  margin: 0;
  padding: 0;
}
.list li {
  width: 400px;
  text-align: left;
  margin: 0.25rem;
  padding: 0.3rem;
  border-radius: 0.5rem;
  background: #89BE31;
  font-size: 1.3em;
}
.list li span {
  margin-left: 0.4rem;
}
.list button {
  border-radius: 0 0.5rem 0.5rem 0;
  border: 0;
  padding: 0.5rem 1.25rem;
  background: #eee;
  font-weight: bold;
  cursor: pointer;
}
#NameSpan{
  font-size: 1.1em;
  color: #eee;
}
</style>
