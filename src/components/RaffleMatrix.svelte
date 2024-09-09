<script>
    export let puestos = Array(100).fill(null); // Recibe los 100 puestos
    export let onPuestoClick; // Función que se llama al hacer clic en un puesto
  
    function getClassForPuesto(index) {
      return puestos[index] ? 'bg-red-500 text-white' : 'bg-green-500 text-black'; // rojo si está vendido, verde si está disponible
    }

  // Función para formatear el número a dos dígitos
  function formatPuesto(index) {
    return String(index).padStart(2, '0'); // Formatea el índice a dos dígitos
  }
  </script>
  
  <div class="grid grid-cols-10 gap-2">
    {#each Array(100) as _, index}
      <button
        class="w-full p-2 rounded text-center cursor-pointer {getClassForPuesto(index)}"
        on:click={() => onPuestoClick(index)}
      >
      {formatPuesto(index)} <!-- Usamos la función para mostrar el índice formateado -->
      </button>
    {/each}
  </div>
  
  <style>
    .bg-green-500 {
      background-color: #22c55e;
    }
    .bg-red-500 {
      background-color: #ef4444;
    }
  </style>
  