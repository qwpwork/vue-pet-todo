<template>
  <v-container class="mt-5">
    <v-form @submit.prevent>
      <v-text-field
        append-icon="mdi-send"
        variant="underlined"
        v-model="inputValue"
        @keyup.enter="addNewItem(inputValue)"
        @click:append="addNewItem(inputValue)"
        clearable
        label="New todo"
      />
    </v-form>
    <p class="text-red mb-3" v-show="isFormHasError == true">
      The input is empty!
    </p>

    <div class="list" v-for="item in itemsList" :key="item.id">
      <v-checkbox
        v-model="item.isChecked"
        v-bind:false-value="false"
        v-bind:true-value="true"
        :label="item.value"
        :value="item.value"
      ></v-checkbox>
    </div>

    <v-btn block @click="removeSelected()">clear selected </v-btn>
  </v-container>
</template>

<script lang="ts">
import { defineComponent } from "vue";
export default defineComponent({
  data() {
    return {
      inputValue: "",
      isFormHasError: false,
      itemsList: [
        { id: 0, value: "Snacks", isChecked: false },
        { id: 1, value: "Some water", isChecked: false },
        { id: 2, value: "Food for pets", isChecked: false },
      ],
    };
  },

  methods: {
    addNewItem(newItem: string) {
      if (this.inputValue != "") {
        this.inputValue = "";
        this.isFormHasError = false;

        this.itemsList.push({
          id: this.itemsList.length,
          value: newItem,
          isChecked: false,
        });
      } else {
        this.isFormHasError = true;
      }
    },

    removeSelected() {
      this.itemsList = this.itemsList.filter((item) => item.isChecked != true);
    },
  },
});
</script>
