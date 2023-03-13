<template>
  <div class="mb-3" ref="selectRef">
    <select
      data-te-select-init
      :data-te-select-placeholder="props.placeholder"
      data-te-select-clear-button="true"
    >
      <option value="" hidden seleted />
      <option
        v-for="option in props.options"
        :key="option.id"
        :value="option.value"
      >
        {{ option.label }}
      </option>
    </select>
    <label data-te-select-label-ref>{{ props.label }}</label>
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted, onBeforeUnmount } from "vue";
import type { Status } from "@/types/articles";

export interface ValueChangeEvent extends CustomEvent {
  value: Status;
}

export interface Props {
  placeholder?: "Placeholder";
  options?: Array<{
    id: string | number;
    value: unknown;
    label: string;
  }>;
  label?: string;
}

const props = withDefaults(defineProps<Props>(), {
  placeholder: "Placeholder",
  options: () => [{ id: 0, value: null, label: "no data" }],
  label: "Example label",
});

const emits = defineEmits<{
  (e: "valueChange", value: Status): void;
}>();

const selectRef = ref<HTMLDivElement>();

const updateSelectValue = (e: Event) =>
  emits("valueChange", (e as ValueChangeEvent).value);

onMounted(() => {
  selectRef.value?.addEventListener("valueChange.te.select", updateSelectValue);
});

onBeforeUnmount(() => {
  selectRef.value?.removeEventListener(
    "valueChange.te.select",
    updateSelectValue
  );
});

function resetSelect() {
  const clearBtn = selectRef.value?.querySelector(
    "span[data-te-select-clear-btn-ref]"
  );
  clearBtn?.dispatchEvent(new Event("click"));
}

defineExpose({
  resetSelect,
});
</script>

<style scoped></style>