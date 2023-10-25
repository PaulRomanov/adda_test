<template>
  <label class="custom-checkbox">
    <input type="checkbox" />
    <span class="checkmark">
      <span class="checked-icon">✔</span>
      <!-- <span v-else-if="checkStatus === false" class="dot-icon">•</span>
      <span v-else-if="checkStatus === null" class="empty-icon"></span> -->
    </span>
  </label>  
</template>

<script>
export default {
  emits: [],
  props: {

  },
  methods: {},
};
</script>

<style scoped>
.custom-checkbox {
  position: relative;
  display: inline-block;
  vertical-align: middle;
  cursor: pointer;
  user-select: none;
  margin-right: 8px;
}

.custom-checkbox input {
  position: absolute;
  opacity: 0;
  cursor: pointer;
  height: 0;
  width: 0;
}

.checkmark {
  position: relative;
  display: inline-block;
  width: 20px;
  height: 20px;
  border: 2px solid #000;
  border-radius: 4px;
  text-align: center;
  line-height: 20px;
  font-size: 16px;
  background-color: #fff;
}

.checked-icon {
  display: none;
}

.dot-icon {
  display: none;
}

.custom-checkbox input:checked + .checkmark .checked-icon {
  display: inline;
}

.custom-checkbox input:not(:checked) + .checkmark .dot-icon {
  display: inline;
}

.empty-icon {
  display: inline;
}
</style>
