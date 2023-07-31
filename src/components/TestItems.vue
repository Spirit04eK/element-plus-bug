<template>
  <div>
    <el-scrollbar :always="false">
      <table class="w-100">
        <colgroup>
          <col
            v-for="(item, index) in headers"
            :width="`${100 / headers.length}%`"
            :key="index">
        </colgroup>

        <thead>
          <tr>
            <th v-for="item in headers">{{ item.title }}</th>
          </tr>
        </thead>

        <slot name="prepend"></slot>

        <tbody>
          <slot v-for="(item, idx) in items" name="item" :item="item" :mobile="true" :key="idx">
            <tr>
              <td>{{ item }}</td>
            </tr>
          </slot>
        </tbody>

      </table>

      <slot name="append"></slot>
    </el-scrollbar>
  </div>
</template>

<script setup>
  const props = defineProps({
    items: {
      type: Array,
      default() {
        return [];
      },
    },
    headers: {
      type: Array,
      default() {
        return [];
      },
    }
  });
</script>