<template>
  <div class="form-container">
    <form @submit.prevent="submitForm" class="form">
      <h1>Formulario de Registro</h1>
      <div class="form-group">
        <label for="name">Nombre:</label>
        <input v-model="formData.name" type="text" id="name" class="form-input" />
        <span v-if="formSubmitted && validateName" class="error">{{ validateName }}</span>
      </div>

      <div class="form-group">
        <label for="lastName">Apellido:</label>
        <input v-model="formData.lastName" type="text" id="lastName" class="form-input" />
        <span v-if="formSubmitted && validateLastName" class="error">{{ validateLastName }}</span>
      </div>

      <div class="form-group">
        <label for="age">Edad:</label>
        <input v-model="formData.age" type="number" id="age" class="form-input" />
        <span v-if="formSubmitted && validateAge" class="error">{{ validateAge }}</span>
      </div>

      <div class="form-group">
        <label for="gender">Género:</label>
        <select v-model="formData.gender" id="gender" class="form-input">
          <option value="masculino">Masculino</option>
          <option value="femenino">Femenino</option>
          <option value="otro">Otro</option>
        </select>
        <span v-if="formSubmitted && validateGender" class="error">{{ validateGender }}</span>
      </div>

      <div v-if="formData.gender === 'otro'" class="form-group">
        <label for="customGender">Género Personalizado:</label>
        <input v-model="customGender" type="text" id="customGender" class="form-input" placeholder="Agregar género personalizado" />
        <span v-if="formSubmitted && validateCustomGender" class="error">{{ validateCustomGender }}</span>
      </div>

      <button type="submit" class="submit-button">Enviar</button>
    </form>

    <div v-if="formSubmitted && !hasValidationErrors" class="submitted-data">
      <h2>Datos enviados:</h2>
      <p>Nombre: {{ formData.name }}</p>
      <p>Apellido: {{ formData.lastName }}</p>
      <p>Edad: {{ formData.age }}</p>
      <p>Género: {{ formData.gender === 'otro' ? customGender : formData.gender }}</p>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const formData = ref({
  name: '',
  lastName: '',
  age: '',
  gender: 'masculino',
});

const customGender = ref('');
const formSubmitted = ref(false);

const validateName = ref('');
const validateLastName = ref('');
const validateAge = ref('');
const validateGender = ref('');
const validateCustomGender = ref('');

const hasValidationErrors = () => {
  return (
    validateName.value ||
    validateLastName.value ||
    validateAge.value ||
    validateGender.value ||
    validateCustomGender.value
  );
};

const submitForm = () => {
  formSubmitted.value = true;

  validateName.value = validateNameFn();
  validateLastName.value = validateLastNameFn();
  validateAge.value = validateAgeFn();
  validateGender.value = validateGenderFn();
  validateCustomGender.value = validateCustomGenderFn();

  if (!hasValidationErrors()) {
    console.log('Formulario enviado:', formData.value);
  }
};

const validateNameFn = () => {
  const name = formData.value.name.trim();
  if (name === '') {
    return 'El nombre no debe estar vacío.';
  } else {
    return (name.length < 5 || name.length > 10) ? 'El nombre debe tener entre 5 y 10 caracteres.' : '';
  }
};


const validateLastNameFn = () => {
  const lastName = formData.value.lastName.trim();
  return formSubmitted.value && lastName === formData.value.name ? 'El apellido no puede ser igual al nombre.' : '';
};

const validateAgeFn = () => {
  const age = parseInt(formData.value.age, 10);
  return formSubmitted.value && (isNaN(age) || age <= 0 || age >= 60) ? 'La edad debe ser mayor a 0 y menor a 60.' : '';
};

const validateGenderFn = () => {
  return formSubmitted.value && (formData.value.gender === 'otro' && customGender.value.trim() === '') ? 'Por favor, ingrese un género personalizado.' : '';
};

const validateCustomGenderFn = () => {
  return formSubmitted.value && (formData.value.gender === 'otro' && customGender.value.trim() === '') ? 'Por favor, ingrese un género personalizado.' : '';
};
</script>

<style scoped>
.form-container {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}

.form {
  max-width: 400px;
  width: 100%;
  padding: 20px;
  border: 1px solid #ccc;
  border-radius: 10px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}

.form-group {
  margin-bottom: 20px;
}

label {
  display: block;
  margin-bottom: 5px;
  font-weight: bold;
}

.form-input {
  width: 100%;
  padding: 10px;
  margin-bottom: 10px;
  border: 1px solid #ccc;
  border-radius: 5px;
}

.error {
  color: red;
  margin-top: 5px;
}

.submit-button {
  background-color: #bfbc0d;
  color: #fff;
  cursor: pointer;
  width: 100%;
  padding: 10px;
  border: none;
  border-radius: 5px;
}

.submit-button:hover {
  background-color: #f0d402;
}

</style>