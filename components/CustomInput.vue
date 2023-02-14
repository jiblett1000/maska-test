<template>
  <div>
    <input
      ref="inputEl"
      v-model="initialValue"
      v-maska:[maskOptions]="maskObject"
      :name="name"
      :id="name"
      :type="type"
      :placeholder="placeholder"
      class=""
    />
  </div>
</template>

<script setup lang="ts">
import { useField } from "vee-validate";
import { vMaska, MaskOptions } from "maska";

interface Props {
  name: string;
  label: string;
  type?: string;
  value?: string;
  backgroundColor?: string;
  placeholder?: string;
  modelValue?: string;
  maskOptions?: MaskOptions;
}

const props = defineProps<Props>();
const name = toRef(props, "name");
const inputEl = ref<HTMLInputElement | null>(null);

const initialValue = ref<string | undefined>(undefined);

const maskObject = reactive({
  masked: "",
  unmasked: "",
  completed: false,
});

const {
  setValue,
  resetField,
  value: inputValue,
} = useField(name, undefined, {
  initialValue: props.value,
  validateOnValueUpdate: false,
});

onMounted(() => {
  if (props.value) {
    initialValue.value = props.value;
  }
});

// Sync vee-validate with maska value
watch(maskObject, (newValue) => {
  setValue(newValue.unmasked);
  console.log(maskObject)
});

// Reset vee-validate and maska
function clearField() {
  Object.assign(maskObject, {
    masked: "",
    unmasked: "",
    completed: false,
  });

  resetField();
}

defineExpose({
  inputEl,
});
</script>
