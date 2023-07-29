<template>
      <v-container>
        <v-card width="500px" height="200px">
          <v-card-title>Date Picker Test</v-card-title>
          <v-card-item>
            <v-row class="mt-2">
              <v-col >
                <v-card-text>
                  <v-text-field
                      v-model="dateOfBirth"
                      type="text"
                      label="*Date of Birth"
                      append-inner-icon="mdi-calendar"
                      :clearable="true"
                      density="compact"
                      variant="outlined"
                      @click:append-inner="showCalendar(true)">
                  </v-text-field>
                </v-card-text>
              </v-col>
            </v-row>
          </v-card-item>
        </v-card>

        <base-dialog
            :is-visible="showDialog"
            @close-calendar="showCalendar(false)"
            @save-value = "dob"
        ></base-dialog>
      </v-container>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue';
import BaseDialog from './components/ui/BaseDialog.vue';
export default defineComponent({
  components: {
    'base-dialog': BaseDialog,
  },
  setup() {
    const showDialog = ref<boolean>(false);
    const dateOfBirth = ref<any>(undefined);
    const showCalendar = (show:boolean) => {
      showDialog.value = show;
    }

    const dob = (val:any) =>{
      console.log("Date of Birth =>", val);
    }

    return {
      showDialog,
      dateOfBirth, showCalendar, dob
    }
  }

})
</script>