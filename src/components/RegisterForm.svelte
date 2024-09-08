<script>
  let name = "";
  console.log("Componente cargado");

  function handleInput(event) {
    console.log("Evento de input capturado", event.target.value);
  }
</script>

<div>
  <h1>Formulario de Registro</h1>
  <input
    type="text"
    bind:value={name}
    on:input={handleInput}
    placeholder="Nombre"
    class="input input-bordered w-full"
  />
</div>
