<!-- Componente de administración de citas médicas -->
<script>
export default {
    data() {
        return {
            patient: '',
            date: '',
            time: '',
            severity: '',
            reason: '',
            appointments: []
        }
    }
}
</script>

<template>
    <h1>Administración de Citas</h1>

    <form class="my-form">
        <div class="sub-container">
            <div class="form-group">
                <label :class="patient ? 'active' : 'waiting'" for="patient">Paciente:</label>
                <input v-model="patient" 
                type="text" id="patient" name="patient" required>
            </div>

            <div class="form-group">
                <label :class="date ? 'active' : 'waiting'" for="date">Fecha:</label>
                <input v-model="date" type="date" id="date" name="date" required>
            </div>

            <div class="form-group">
                <label :class="time ? 'active' : 'waiting'" for="time">Hora:</label>
                <input v-model="time" type="time" id="time" name="time" required>
            </div>

            <div class="form-group">
                <label :class="severity ? 'active' : 'waiting'" for="severity">Gravedad:</label>
                <select v-model="severity" id="severity" name="severity" required>
                    <option value="leve">Leve</option>
                    <option value="media">Media</option>
                    <option value="grave">Grave</option>
                </select>
            </div>

            <div class="form-group">
                <label :class="reason ? 'active' : 'waiting'" for="reason">Motivo:</label>
                <input v-model="reason" type="textarea" id="reason" name="reason" required></input>
            </div>

        </div>

        <button style="margin-top: 2rem;" :disabled="!patient || !date || !time || !severity || !reason" v-on:click="appointments.push({patient, date, time, severity, reason})" type="submit" class="btn btn-primary">Agregar</button>
    </form>
    <!-- Cuando no hay citas ingresadas se muestra este mensaje -->
    <p v-if="!appointments.length" class="no-appointments">Aún no hay consultas registradas</p>
    
    <!-- Aquí se mostrará las cards resumen con la ficha de las citas agendadas -->
    <div class="cards-container" @submit.prevent>
        <div v-for="appointment in appointments">
            <p>Paciente: {{ appointment.patient }}</p>
            <p>Fecha: {{ appointment.date }}</p>
            <p>Hora: {{ appointment.time }}</p>
            <p>Gravedad: {{ appointment.severity }}</p>
            <p>Motivo: {{ appointment.reason }}</p>
            <button @click="appointments.splice(appointments.indexOf(appointment), 1)" >Eliminar</button>
        </div>
    </div>


</template>

<style scoped>

.form-group {
    display: flex;
    flex-direction: column;
    gap: .25rem;
}

.my-form {
    display: flex;
    flex-direction: column;
    align-items: center;
    border: 1px solid black;
    padding: 1rem;
    border-radius: 8px;
    gap: .5rem;
    max-width: 80%;
    }

.sub-container {
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    gap: 1rem;
    }

.no-appointments {
    color: red;
    font-weight: 600;
    font-size: 1.25rem;
    text-align: center;
    margin-top: 1rem;
}

.waiting {
    color: red ;
    font-weight: 600;
}

.cards-container {
    display: grid; 
    grid-template-columns: repeat(3, 1fr);
}

.severity-low {
    background-color: green;
}

.severity-mid {
    background-color: yellow;
}

.severity-high {
    background-color: red;
}

h1 {
    text-align: center;
}

</style>