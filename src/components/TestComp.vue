<template>
  <test-template>
    <test-card>
      <template v-if="visibleTitle" #title>
        <h1>My title</h1>
      </template>

      <div>
        <test-template>
          <button @click="visibleTitle = !visibleTitle">Change title state</button>
          <button @click="onRemove">Remove</button>
          <button @click="onAdd">Add</button>
        </test-template>

        <test-items :headers="headers" :items="[]">
          <template #item="{item}">
            <tr>
              <td>{{ item }}</td>
            </tr>
          </template>
        </test-items>

      </div>
    </test-card>
  </test-template>
</template>

<script>
  export default {
    name: "Index"
  }
</script>

<script setup>
  import { shallowRef, unref, computed } from "vue";
  import TestTemplate from "@/components/TestTemplate.vue";
  import TestCard from "@/components/TestCard.vue";
  import TestItems from "@/components/TestItems.vue";

  const visibleTitle = shallowRef(false);
  const arr = shallowRef(['test-1', 'test-2', 'test-3', 'test-4', 'test-5']);

  const headers = computed(() => {
    return unref(arr).map(v => ({
      title: v,
      key: v,
      fr: 1,
    }));
  });

  function onRemove() {
    const newArr = unref(arr).map(v => v);
    newArr.splice(newArr.length - 1, 1);
    arr.value = newArr;
  }

  function onAdd() {
    const newArr = unref(arr).map(v => v);
    newArr.push(`test-${newArr.length + 1}`);
    arr.value = newArr;
  }
</script>