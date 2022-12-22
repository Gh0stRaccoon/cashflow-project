<template>
  <div class="movement">
    <div class="content">
      <h4>{{ props.movement.title }}</h4>
      <p>{{ props.movement.description }}</p>
    </div>
    <div class="action">
      <img src="@/assets/icons/trash-icon.svg" alt="borrar" @click="remove" />
      <p :class="{ red: isNegative, green: !isNegative }">
        {{ amountCurrency }}
      </p>
    </div>
  </div>
</template>

<script setup>
import { defineProps, computed, defineEmits } from "vue";
import { currencyFormatter } from "@/helpers/currencyFormatter.js";

const props = defineProps({
  movement: {
    type: Object,
  },
});

const emit = defineEmits(["remove"]);

const remove = () => emit("remove", props.movement.id);

const amountCurrency = computed(() =>
  currencyFormatter.format(props.movement.amount)
);

const isNegative = computed(() => props.movement.amount < 0);
</script>

<style scoped>
.movement {
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 100%;
  padding: 16px;
  background-color: #e6f9ff;
  border-radius: 8px;
  box-sizing: border-box;
}
.movement .content {
  width: 100%;
}
.movement .action {
  display: flex;
  justify-content: space-between;
  align-items: flex-end;
  flex-direction: column;
}
h4,
p {
  margin: 0;
  padding: 0;
}
h4 {
  margin-bottom: 8px;
}
.movement .action img {
  margin-bottom: 16px;
}
.red {
  color: red;
}
.green {
  color: green;
}
</style>
