<template>
  <div class="modal-overlay" @click.self="$emit('close')">
    <div class="modal-content">
      <h3>¿Qué quieres ver?</h3>
      <div class="options">
        <button @click="$emit('view-dashboard')">Ver Dashboard</button>
        <button @click="$emit('view-details')">Ver Detalles</button>
      </div>
      <button @click="eliminarCosplay" class="delete-button">Eliminar</button>
      <button @click="$emit('close')" class="close-button">Cerrar</button>

    </div>
  </div>
</template>

<script setup>
import { defineProps, defineEmits } from 'vue';
import axios from 'axios';



const emit = defineEmits(['close', 'view-dashboard', 'view-details', 'cosplay-eliminado']);



const eliminarCosplay = async () => {

  try {
    await axios.delete(`http://localhost:3000/deleteCosplays/${localStorage.selectedCosplay}`);
    emit('cosplay-eliminado', localStorage.selectedCosplay); // Emitir evento al padre
    emit('close'); // Cerrar el modal después de la eliminación
    location.reload();
  } catch (error) {
    console.error('Error al eliminar el cosplay:', error);
    alert('Hubo un error al intentar eliminar el cosplay.');
  }
};
</script>

<style scoped>
.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.2);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 1010;
  padding-left: 18vw;
  padding-right: 1vw;
  padding-top: 10vh;
  padding-bottom: 3vh;
  box-sizing: border-box;

}

.modal-content {
  background-color: var(--mainColor);
  padding: 30px;
  border-radius: 12px;
  box-shadow: 0 5px 15px rgba(0, 0, 0, 0.2);
  text-align: center;
  width: 100%;
  max-width: 380px;
  box-sizing: border-box;
  border: 2px solid var(--secondaryColor);
}

h3 {
  color: var(--secondaryColor);
  margin-bottom: 25px;
  /* Más espacio debajo del título */
  font-size: 1.5em;
  /* Tamaño de fuente del título */
  font-weight: 600;
}

.options {
  display: flex;
  flex-direction: column;
  /* Apila los botones verticalmente */
  gap: 12px;
  /* Espacio entre botones */
  margin-bottom: 25px;
  /* Espacio entre el grupo de opciones y los botones de acción */
}

/* Estilo base para todos los botones del modal */
.modal-content button {
  padding: 12px 20px;
  /* Padding para hacer los botones más grandes */
  border: 2px solid var(--secondaryColor);
  border-radius: 8px;
  /* Bordes redondeados */
  cursor: pointer;
  font-size: 1em;
  /* Tamaño de fuente consistente */
  font-weight: 600;
  transition: background-color 0.3s ease, transform 0.2s ease, box-shadow 0.2s ease;
  width: 100%;
  /* Para que ocupen todo el ancho disponible en la columna */
}


.options button {
  background-color: var(--modalNuevo);
  border: 2px solid var(--secondaryColor);
  color: var(--secondaryColor);
}

.options button:hover {
  background-color: var(--complementaryColor);
  transform: translateY(-2px);
  box-shadow: 0 4px 10px rgba(106, 13, 173, 0.2);
  /* Sombra con el color del botón */
}

/* Estilo para el botón "Cerrar" (secundario) */
.close-button {
  background-color: var(--secondaryColor);
  color: var(--mainColor);
  border: 1px solid var(--complementaryColor3);
  margin-top: 15px;
  /* Espacio entre el último botón de opción y el botón cerrar */
}

.close-button:hover {
  background-color: var(--secondaryColor);
  transform: translateY(-1px);
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
}

/* Estilo para el botón "Eliminar" (peligro) */
.delete-button {
  background-color: var(--complementaryColor);
  border: 2px solid var(s);
  color: var(--secondaryColor);
  margin-top: 10px;
}

.delete-button:hover {

  transform: translateY(-2px);
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.2);
}
</style>