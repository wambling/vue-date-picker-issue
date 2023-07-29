<template>
    <teleport to="body">
        <v-dialog :model-value="isVisible" width="auto">
          <v-date-picker
              v-model="date"
              style="{font-size: 20px}"
              title="Date of Birth"
              calendarIcon="mdi-calendar-account"
              collapseIcon="mdi-calendar-collapse-horizontal"
              expandIcon="mdi-calendar-expand-horizontal"
              keyboardIcon="mdi-keyboard"
              showAdjacentMonths
              elevation="20"
              color="primary"
              @click:cancel="closeCalendar"
              @click:save="saveValue"
              :min="1900"
              :max="2024"
          ></v-date-picker>
        </v-dialog>
    </teleport>
</template>

<script lang="ts">
import { defineComponent, ref, watch } from 'vue';
import { VDatePicker } from 'vuetify/labs/components';
export default defineComponent({
    components: {
        'v-date-picker': VDatePicker
    },
  emits:['close-calendar', 'save-value'],
    props: {
        isVisible: {
            type: Boolean,
            required: true
        }
    },
    setup(props, context) {
      const date = ref<any>(undefined);

      watch(date, (newValue)=> {
        console.log('Base Dialog Watch => ', newValue);
      })
      const closeCalendar = ()=> {
        context.emit('close-calendar');
      };
      const saveValue = () => {
        context.emit('save-value', date.value);
        closeCalendar();
      }
      return {
        date, closeCalendar, saveValue
      }
    }
})
</script>