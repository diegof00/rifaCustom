<script>
    export let isOpen = false; // Controla si el popup está visible
    export let puestoIndex; // El puesto seleccionado
    export let onClose; // Función para cerrar el popup
    export let onSave; // Función para guardar los datos del comprador
  
    let nombre = '';
    let telefono = '';
    let pagado = false;
  
    function handleSave() {
      onSave({ puestoIndex, nombre, telefono, pagado }); // Llamamos la función para guardar los datos
      onClose(); // Cerramos el popup
    }
  </script>
  
  {#if isOpen}
    <div class="fixed inset-0 bg-black bg-opacity-50 flex justify-center items-center">
      <div class="bg-base-200 p-6 rounded shadow-lg max-w-md w-full">
        <h2 class="text-2xl font-bold mb-4 text-primary">Puesto {puestoIndex}</h2>
  
        <label for="nombre" class="block text-accent mb-2">Nombre</label>
        <input id="nombre" class="input input-bordered w-full p-2 mb-4" type="text" bind:value={nombre} />
  
        <label for="telefono" class="block text-accent mb-2">Teléfono</label>
        <input id="telefono" class="input input-bordered w-full p-2 mb-4" type="tel" bind:value={telefono} />
  
        <label class="flex items-center text-accent mb-4">
          <input id="pagado" type="checkbox" bind:checked={pagado} class="checkbox checkbox-primary mr-2" />
          Pagado
        </label>
  
        <div class="flex justify-between">
          <button class="btn btn-error" on:click={onClose}>Cancelar</button>
          <button class="btn btn-success" on:click={handleSave}>Guardar</button>
        </div>
      </div>
    </div>
  {/if}
  