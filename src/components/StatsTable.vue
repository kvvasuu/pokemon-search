<template>
  <div class="table-container">
    <table id="stats-table">
      <tbody id="stats">
        <tr>
          <th class="base">Base</th>
          <th>Stats</th>
        </tr>
        <tr>
          <td class="base">HP:</td>
          <td id="hp">{{ stat[0].base_stat }}</td>
        </tr>
        <tr>
          <td class="base">Attack:</td>
          <td id="attack">{{ stat[1].base_stat }}</td>
        </tr>
        <tr>
          <td class="base">Defense:</td>
          <td id="defense">{{ stat[2].base_stat }}</td>
        </tr>
        <tr>
          <td class="base">Sp. Attack:</td>
          <td id="special-attack">{{ stat[3].base_stat }}</td>
        </tr>
        <tr>
          <td class="base">Sp. Defense:</td>
          <td id="special-defense">{{ stat[4].base_stat }}</td>
        </tr>
        <tr>
          <td class="base">Speed:</td>
          <td id="speed" class="speed">{{ stat[5].base_stat }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  props: ["stat"],
};
</script>

<style scoped>
.table-container {
  background-color: var(--background-transparent);
  color: var(--black);
  border-radius: 0.3rem;
  width: 25rem;
  margin: 1rem 0 2rem 0;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  box-shadow: 0 0 0.625rem rgba(0, 0, 0, 0.3);
  backdrop-filter: blur(5px);
}

table {
  margin: 0.5rem 0.5rem;
  border-radius: 0.2rem;
  border-collapse: collapse;
  width: 24rem;
  overflow: hidden;
  box-shadow: 0 0 0.625 rgba(0, 0, 0, 0.3);
  text-align: center;
  text-shadow: 0.1rem 0.1rem 0.05rem var(--poke-blue);
  background-color: rgba(255, 255, 255, 0.2);
}

th,
td {
  color: var(--poke-yellow);
  padding: 0.3rem;
  text-align: center;
}

th {
  text-align: center;
}
</style>
