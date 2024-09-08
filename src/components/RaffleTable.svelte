<script>
    // Datos de ejemplo
    export let raffles = [
        { name: 'Rifa 1', soldSpots: 10, totalSpots: 100, status: 'activa' },
        { name: 'Rifa 2', soldSpots: 50, totalSpots: 50, status: 'finalizada' },
        { name: 'Rifa 3', soldSpots: 20, totalSpots: 60, status: 'borrador' },
        { name: 'Rifa 4', soldSpots: 5, totalSpots: 10, status: 'inactiva' },
        { name: 'Rifa 5', soldSpots: 25, totalSpots: 100, status: 'activa' },
    ];

    // Función para obtener el porcentaje de puestos vendidos
    function getPercentage(sold, total) {
        return (sold / total) * 100;
    }

    // Función para obtener las clases de estilo basadas en el estado
    function getStatusClass(status) {
        switch (status) {
            case 'activa':
                return 'badge badge-success'; // Verde para activa
            case 'inactiva':
                return 'badge badge-error'; // Rojo para inactiva
            case 'borrador':
                return 'badge badge-warning'; // Amarillo para borrador
            case 'finalizada':
                return 'badge badge-neutral'; // Gris para finalizada
            default:
                return '';
        }
    }
</script>

<table class="table w-full">
    <thead>
        <tr>
            <th>Nombre de la Rifa</th>
            <th>Puestos Vendidos/Puestos Disponibles</th>
            <th>Progreso (%)</th>
            <th>Estado</th>
        </tr>
    </thead>
    <tbody>
        {#each raffles as raffle}
            <tr>
                <td>{raffle.name}</td>
                <td>{raffle.soldSpots}/{raffle.totalSpots}</td>
                <td>{getPercentage(raffle.soldSpots, raffle.totalSpots).toFixed(2)}%</td>
                <td><span class={getStatusClass(raffle.status)}>{raffle.status}</span></td>
            </tr>
        {/each}
    </tbody>
</table>
