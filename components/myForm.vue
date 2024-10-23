<script setup lang="ts">

const emit = defineEmits<{
  (event: 'submit'): void,
}>();

const formState = reactive<{ title: string }>({
  title: '',
});

</script>

<template>
  <a-form :model="formState" @finish="emit('submit')">
    <a-form-item name="title" label="title">
      <a-input :maxlength=30 ref="ainput" v-model="formState.title" autocomplete="off"/>
    </a-form-item>
    <a-form-item>
      <a-button type="primary" html-type="submit" style="min-width: 200px">Ok</a-button>
    </a-form-item>
  </a-form>
</template>

<style scoped>

</style>