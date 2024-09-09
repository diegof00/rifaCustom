<script>
  let premio = "";
  let loteria = "loteria de boyaca";
  let fechaSorteo = "";

  const loterias = [
    "loteria de boyaca",
    "loteria de santander",
    "loteria de bogotá",
  ];

  const crearRifa = () => {
    console.log("Rifa creada:", { premio, loteria, fechaSorteo });
    // Aquí puedes manejar el evento, como enviar los datos a una API o cambiar el estado en Astro
    alert(
      `Rifa creada con premio: ${premio}, Lotería: ${loteria}, fecha: ${fechaSorteo}`
    );
  };
</script>

<form
  on:submit|preventDefault={crearRifa}
  class="max-w-md mx-auto p-6 bg-base-200 rounded shadow-md"
>
  <div class="form-control mb-4">
    <label class="label text-base-content">
      <span class="label-text">Premio</span>
    </label>
    <input
      id="premio"
      type="text"
      bind:value={premio}
      required
      class="input input-bordered w-full"
      placeholder="Ingresa el premio"
    />
  </div>

  <div class="form-control mb-4">
    <label class="label text-base-content">
      <span class="label-text">Lotería</span>
    </label>
    <select
      id="loteria"
      bind:value={loteria}
      required
      class="select select-bordered w-full"
    >
      {#each loterias as loteriaOption}
        <option value={loteriaOption}>{loteriaOption}</option>
      {/each}
    </select>
  </div>

  <div class="form-control mb-4">
    <label class="label text-base-content">
      <span class="label-text">Fecha del sorteo</span>
    </label>
    <input
      id="fechaSorteo"
      type="date"
      bind:value={fechaSorteo}
      min={new Date().toISOString().split("T")[0]}
      required
      class="input input-bordered w-full"
    />
  </div>

  <div class="text-center">
    <button type="submit" class="btn btn-primary btn-block">
      Crear Rifa
    </button>
  </div>
</form>
