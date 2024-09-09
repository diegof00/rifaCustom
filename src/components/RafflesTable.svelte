<script>
  // Datos de ejemplo directamente en el componente Svelte

  export let raffles = [
    { id: 1, name: "Rifa 1", premio: "Moto Honda", soldSpots: 10, totalSpots: 100, loteria: "Lotería de Boyacá", fechaSorteo: "2024-09-18", status: "activa" },
    { id: 2, name: "Rifa 2", premio: "Moto Suzuki", soldSpots: 50, totalSpots: 50, loteria: "Lotería de Bogotá", fechaSorteo: "2024-10-05", status: "finalizada" },
    { id: 3, name: "Rifa 3", premio: "Whiskey Johnnie Walker", soldSpots: 20, totalSpots: 60, loteria: "Lotería del Huila", fechaSorteo: "2024-09-25", status: "borrador" },
    { id: 4, name: "Rifa 4", premio: "Whiskey Glenfiddich", soldSpots: 5, totalSpots: 10, loteria: "Lotería de Boyacá", fechaSorteo: "2024-10-15", status: "inactiva" },
    { id: 5, name: "Rifa 5", premio: "Moto Yamaha", soldSpots: 25, totalSpots: 100, loteria: "Lotería de Bogotá", fechaSorteo: "2024-11-01", status: "activa" }
  ];

  function getPercentage(sold, total) {
    return (sold / total) * 100;
  }

  function getStatusClass(status) {
    switch (status) {
      case "activa":
        return "badge badge-success"; // Verde para activa
      case "inactiva":
        return "badge badge-error"; // Rojo para inactiva
      case "borrador":
        return "badge badge-warning"; // Amarillo para borrador
      case "finalizada":
        return "badge badge-neutral"; // Gris para finalizada
      default:
        return "";
    }
  }
</script>

<table class="table w-full">
  <thead>
    <tr>
      <th>Id</th>
      <th>Nombre de la Rifa</th>
      <th>Premio</th>
      <th class="w-1/6">Puestos Vendidos/Puestos Disponibles</th>
      <th class="w-1/6">Progreso (%)</th>
      <th class="w-1/6">Lotería</th>
      <th class="w-1/6">Fecha Sorteo</th>
      <th class="w-1/8">Estado</th>
    </tr>
  </thead>
  <tbody>
    {#each raffles as raffle}
      <tr
        on:click={() => (window.location.href = `/raffle/${raffle.id}`)}
        class="cursor-pointer"
      >
        <td>{raffle.id}</td>
        <td>{raffle.name}</td>
        <td>{raffle.premio}</td>
        <td>{raffle.soldSpots}/{raffle.totalSpots}</td>
        <td>{getPercentage(raffle.soldSpots, raffle.totalSpots).toFixed(2)}%</td
        >
        <td>{raffle.loteria}</td>
        <td>{raffle.fechaSorteo}</td>
        <td
          ><span class={getStatusClass(raffle.status)}>{raffle.status}</span
          ></td
        >
      </tr>
    {/each}
  </tbody>
</table>
