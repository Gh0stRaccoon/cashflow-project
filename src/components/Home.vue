<template>
  <Layout>
    <template #header>
      <Header></Header>
    </template>
    <template #resume>
      <Resume
        :label="'Ahorro total'"
        :amount="selectedAmount"
        :total-amount="totalAmount"
      >
        <template #graphic>
          <Graphic :amounts="amounts" @select="select" />
        </template>
        <template #action>
          <Action @create="create" />
        </template>
      </Resume>
    </template>
    <template #movements>
      <Movements :movements="movements" @remove="remove"></Movements>
    </template>
  </Layout>
</template>

<script setup>
import Layout from "./Layout.vue";
import Header from "./Header.vue";
import Resume from "./Resume/Index.vue";
import Graphic from "./Resume/Graphic.vue";
import Movements from "./Movements/Index.vue";
import Action from "./Action.vue";
import { ref, computed, onMounted } from "vue";

const save = () => {
  localStorage.setItem("movements", JSON.stringify(movements.value));
};

const create = (movement) => {
  movements.value.push(movement);
  save();
};

const remove = (id) => {
  movements.value = movements.value.filter((el) => el.id !== id);
  save();
};

const selectedAmount = ref(0);
const select = (e) => (selectedAmount.value = e);

const movements = ref([]);

const amounts = computed(() => {
  const lastDays = movements.value
    .filter((el) => {
      const today = new Date();
      const oldDate = today.setDate(today.getDate() - 30);

      return el.time >= oldDate;
    })
    .map((el) => el.amount);

  return lastDays.map((el, i) => {
    const lasMovements = lastDays.slice(0, i + 1);

    return lasMovements.reduce((acc, cur) => acc + cur, 0);
  });
});

const totalAmount = computed(() =>
  movements.value.reduce((acc, cur) => acc + cur.amount, 0)
);

onMounted(() => {
  const localMovements = JSON.parse(localStorage.getItem("movements"));
  if (Array.isArray(localMovements)) {
    movements.value = localMovements?.map((el) => ({
      ...el,
      time: new Date(el.time),
    }));
  }
});
</script>
