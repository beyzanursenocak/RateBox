<template>
  <div class="rate-box">
    <span
      v-for="i in 5"
      :key="i"
      class="star"
      :class="{ filled: i <= currentRating || (editable && i <= hoverRating) }"
      @mouseover="onMouseover(i)"
      @mouseleave="onMouseleave"
      @click="onClick(i)"
    >
      ★
    </span>
  </div>
</template>

<script setup>
import { ref, defineEmits, defineProps, watch } from 'vue';

const props = defineProps({
  modelValue: Number,
  editable: Boolean
});

const emit = defineEmits(['update:modelValue']);

const currentRating = ref(props.modelValue);
const hoverRating = ref(0);

const onMouseover = (rating) => {
  if (props.editable) {
    hoverRating.value = rating;
  }
};

const onMouseleave = () => {
  hoverRating.value = 0;
};

const onClick = (rating) => {
  if (props.editable) {
    const newValue = (rating === currentRating.value) ? 0 : rating;
    currentRating.value = newValue;
    emit('update:modelValue', newValue);
  }
};

watch(() => props.modelValue, (newValue) => {
  currentRating.value = newValue;
});
</script>

<style scoped>
.rate-box {
  display: inline-flex;
}

.star {
  font-size: 24px;
  cursor: pointer;
  color: #ccc;
}

.star.filled {
  color: gold;
}
</style>
