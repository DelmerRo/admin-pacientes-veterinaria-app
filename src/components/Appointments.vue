<template lang="html">
  <section class="table-responsive">
    <h2 class="text-center my-2 text-success">Citas Pendientes</h2>
    <table v-if="mostrarCitasPendientes.length" class="table table-dark">
      <tr>
        <th>Nombre de Mascota</th>
        <th>Nombre de Dueño</th>
        <th>Fecha atención</th>
        <th>Email</th>
        <th>Síntomas</th>
        <th></th>
      </tr>
      <tr v-for="cita in mostrarCitasPendientes" :key="cita.id">
        <td>{{ cita.nombre }}</td>
        <td>{{ cita.nombre_duenio }}</td>
        <td>{{ cita.fecha_hora_atencion }}</td>
        <td>{{ cita.email }}</td>
        <td>{{ cita.sintomas }}</td>
        <td class="d-flex justify-content-center">
          <button class="btn btn-success mr-1" @click="pasarAHistorial(cita)">
            Atendido
          </button>
          <button class="btn btn-secondary mr-1" @click="editarCita(cita)">
            Editar
          </button>
          <button class="btn btn-danger" @click="eliminarCita(cita.id)">
            Eliminar
          </button>
        </td>
      </tr>
    </table>

    <h4 v-else-if="!mostrarCitasPendientes.length" class="alert alert-info">
      <span>No hay citas pendientes</span>
    </h4>
  </section>
</template>

<script lang="js">

  export default  {
    name: 'appointments-view',
    props: [],
    mounted () {
      this.obtenerCitas();
    },
    data () {
      return {
        url: "https://62b25de3c7e53744afcb7292.mockapi.io/admin-vet/citas/"      }
    },
    methods: {
      pasarAHistorial(cita) {
        let citaAtendida = {
          ...cita,
          atendido: true
        }
        this.editarCitaPendiente(citaAtendida, cita.id);
      },
      editarCita(cita) {
        this.$router.push({ name: 'addappointment', params: { citaAEditar: cita } });
      },
      eliminarCita(id) {
        this.eliminarCitaPendiente(id);
        this.$swal({
        icon: 'success',
        title: 'Cita eliminada exitosamente',
      });
      }
    },
    computed: {

    }
}
</script>

<style scoped lang="css">
tr td {
  color: white;
}
</style>
