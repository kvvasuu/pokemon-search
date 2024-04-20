<template>
  <table id="stats-table">
    <tbody id="stats">
      <tr>
        <th>Base</th>
        <th>Stats</th>
      </tr>
      <tr>
        <td>HP:</td>
        <td id="hp">{{ stat[0].base_stat }}</td>
      </tr>
      <tr>
        <td>Attack:</td>
        <td id="attack">{{ stat[1].base_stat }}</td>
      </tr>
      <tr>
        <td>Defense:</td>
        <td id="defense">{{ stat[2].base_stat }}</td>
      </tr>
      <tr>
        <td>Sp. Attack:</td>
        <td id="special-attack">{{ stat[3].base_stat }}</td>
      </tr>
      <tr>
        <td>Sp. Defense:</td>
        <td id="special-defense">{{ stat[4].base_stat }}</td>
      </tr>
      <tr>
        <td>Speed:</td>
        <td id="speed" class="speed">{{ stat[5].base_stat }}</td>
      </tr>
    </tbody>
  </table>
</template>

<script>
export default {
  props: ["stat"],
};
</script>

<style>
table {
  margin: 1rem 0;
  border-radius: 0.3rem;
  width: 25rem;
  border-collapse: collapse;
  overflow: hidden;
  box-shadow: 0 0 0.625 rgba(0, 0, 0, 0.3);
  text-align: center;
  text-shadow: 0.15rem 0.15rem 0.15rem #000;
}

th,
td {
  color: var(--poke-yellow);
  padding: 0.3rem;
  background-color: var(--background-transparent);
  text-align: center;
}

th {
  text-align: center;
}
</style>
