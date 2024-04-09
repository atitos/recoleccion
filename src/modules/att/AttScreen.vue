<template>
  <q-page class="q-ma-md">
    <span class="text-h3"> ATT Data Colector </span>
    <q-separator spaced />
    <div class="row justify-center">
      <q-form
        @submit="onSubmit"
        @reset="onReset"
        class="q-gutter-md col-xs-6 col-sm-6 col-md-6 q-pt-xl"
      >
        <q-select
          filled
          v-model="serviceType"
          label="Typo de Servicio"
          :options="serviceTypeOptions"
        />
        <q-select
          filled
          v-model="service"
          label="Servicio"
          :options="serviceOptions"
        />

        <div class="row justify-end">
          <q-btn label="Submit" type="submit" color="primary"/>
          <q-btn label="Reset" type="reset" color="primary" flat class="q-ml-sm" />
        </div>
      </q-form>
    </div>
  </q-page>
</template>

<script>
import { defineComponent, ref, watch } from 'vue';
import { useQuasar } from 'quasar'

export default defineComponent({
  name: 'AttRecolectorDeDatos',
  setup() {
    const serviceType = ref(null);
    const service = ref(null);
    const serviceTypeOptions = ref(['Servicios Móviles', 'Servicios Fijos']);
    const serviceOptions = ref([]);

    watch(serviceType, (newValue) => {
      if (newValue === 'Servicios Móviles') {
        serviceOptions.value = [
          {label:'Internet', value: 1},
          {label:'Servicio Movil Prepago', value: 2}
        ];
      } else if (newValue === 'Servicios Fijos') {
        serviceOptions.value = [
          {label:'Internet', value: 3},
          {label:'Servicio Local Telefonia',value: 4}
        ];
      }
    });

    return {
      serviceType,
      service,
      serviceTypeOptions,
      serviceOptions,

      onSubmit() {
        console.log({serviceType: serviceType.value, service: service.value.value})
      },
      onReset() {
        serviceType.value = null;
        service.value = null;
        serviceTypeOptions.value = ['Servicios Móviles', 'Servicios Fijos'];
        serviceOptions.value = [];
      }
    }
  },
});
</script>
