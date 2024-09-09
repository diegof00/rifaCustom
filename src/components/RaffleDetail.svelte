<script>
  import MatrizPuestos from "./RaffleMatrix.svelte";
  import PopUp from "./PopUpSpot.svelte";

  export let id; // El ID se pasa desde la página de Astro

  // Datos de ejemplo directamente en el componente Svelte
  let raffles = [
    {
      id: 1,
      name: "Rifa 1",
      premio: "Moto Honda",
      soldSpots: 10,
      paidSpots: 10,
      totalSpots: 100,
      loteria: "Lotería de Boyacá",
      fechaCreacion: "2024-08-01",
      fechaSorteo: "2024-09-18",
      status: "activa",
    },
    {
      id: 2,
      name: "Rifa 2",
      premio: "Moto Suzuki",
      soldSpots: 50,
      paidSpots: 10,
      totalSpots: 50,
      loteria: "Lotería de Bogotá",
      fechaCreacion: "2024-08-01",
      fechaSorteo: "2024-10-05",
      status: "finalizada",
    },
    {
      id: 3,
      name: "Rifa 3",
      premio: "Whiskey Johnnie Walker",
      soldSpots: 20,
      paidSpots: 10,
      totalSpots: 60,
      loteria: "Lotería del Huila",
      fechaCreacion: "2024-08-01",
      fechaSorteo: "2024-09-25",
      status: "borrador",
    },
    {
      id: 4,
      name: "Rifa 4",
      premio: "Whiskey Glenfiddich",
      soldSpots: 5,
      paidSpots: 5,
      totalSpots: 10,
      loteria: "Lotería de Boyacá",
      fechaCreacion: "2024-08-01",
      fechaSorteo: "2024-10-15",
      status: "inactiva",
    },
    {
      id: 5,
      name: "Rifa 5",
      premio: "Moto Yamaha",
      soldSpots: 25,
      paidSpots: 25,
      totalSpots: 100,
      loteria: "Lotería de Bogotá",
      fechaCreacion: "2024-08-01",
      fechaSorteo: "2024-11-01",
      status: "activa",
    },
  ];

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

  // Encontrar la rifa por ID
  let raffle = raffles.find((r) => r.id == id);

  // Control de los puestos (disponible o vendido)
  let puestos = Array(100).fill(null); // Inicializamos 100 puestos vacíos

  // Estado para abrir/cerrar el popup
  let isPopupOpen = false;
  let selectedPuestoIndex = null;

  // Función para abrir el popup cuando se hace clic en un puesto
  function handlePuestoClick(index) {
    console.log("clic en " + index);
    selectedPuestoIndex = index;
    isPopupOpen = true;
  }

  // Función para guardar la información del comprador
  function handleSavePuesto({ puestoIndex, nombre, telefono, pagado }) {
    puestos[puestoIndex] = { nombre, telefono, pagado }; // Guardar información del comprador
    isPopupOpen = false; // Cerrar el popup después de guardar
  }

  // Función para cerrar el popup sin guardar
  function handleClosePopup() {
    isPopupOpen = false;
  }
</script>

{#if raffle}
  <div class="border p-6 rounded-md shadow-md max-w-6xl mx-auto bg-base-300">
    <h3 class="text-center text-3xl font-bold mb-6">
      Detalles de {raffle.name}
    </h3>
    <div class="grid grid-cols-3 gap-6">
      <p class="text-lg"><strong>Id:</strong> {raffle.id}</p>
      <p class="text-lg"><strong>Premio:</strong> {raffle.premio}</p>
      <p class="text-lg">
        <strong>Puestos vendidos:</strong>
        {raffle.soldSpots}/{raffle.totalSpots}
      </p>
      <p class="text-lg">
        <strong>Puestos pagados:</strong>
        {raffle.paidSpots}/{raffle.totalSpots}
      </p>
      <p class="text-lg">
        <strong>Progreso:</strong>
        {((raffle.soldSpots / raffle.totalSpots) * 100).toFixed(2)}%
      </p>
      <p class="text-lg"><strong>Lotería:</strong> {raffle.loteria}</p>
      <p class="text-lg">
        <strong>Fecha del Sorteo:</strong>
        {raffle.fechaSorteo}
      </p>
      <p class="text-lg">
        <strong>Fecha de Creación:</strong>
        {raffle.fechaCreacion}
      </p>
      <p class="text-lg">
        <strong>Estado:</strong>
        <span class={getStatusClass(raffle.status)}>{raffle.status}</span>
      </p>
    </div>
    <div class="mt-6 text-center">
      <a href="/raffles" class="btn btn-primary">
        Volver a la lista de rifas
      </a>
      <a href="/raffles" class="btn btn-secondary">
        Editar Rifa {raffle.name}
      </a>
    </div>
  </div>
{:else}
  <p>No se encontró la rifa</p>
{/if}

<!-- Agregar la Matriz de Puestos debajo de los detalles -->
<div class="mt-6">
  <h3 class="text-center text-2xl font-bold mb-4">Puestos Disponibles</h3>
  <MatrizPuestos {puestos} onPuestoClick={handlePuestoClick} client=load />
</div>

<!-- Popup para ingresar datos del comprador -->
<PopUp client=load
  isOpen={isPopupOpen}
  puestoIndex={selectedPuestoIndex}
  onClose={handleClosePopup}
  onSave={handleSavePuesto}
/>
