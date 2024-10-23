<script setup lang="ts">

const popupOpen = ref(false)
const popupContentRef = ref(null)

let clickOutsideCleaner: ReturnType<typeof onClickOutside>;
let escListenerCleaner: ReturnType<typeof useEventListener>;


function openPopup() {
  popupOpen.value = true;
  escListenerCleaner = useEventListener(document, 'keydown', closeByEsc);
  clickOutsideCleaner = onClickOutside(popupContentRef, closePopup)
}

function closePopup() {
  popupOpen.value = false;
  escListenerCleaner();
  clickOutsideCleaner();
}

function togglePopup() {
  if (popupOpen.value) closePopup();
  else openPopup();
}

function closeByEsc(evt: KeyboardEvent) {
  if (evt.key === 'Escape') closePopup();
}

defineExpose({
  openPopup,
  closePopup,
  togglePopup
})

</script>

<template>
  <a-popover :open="popupOpen">
    <template #content>
      <div ref="popupContentRef">
        <slot name="form" :closePopup="closePopup"></slot>
      </div>
    </template>
    <slot name="trigger" :openPopup="togglePopup"></slot>
  </a-popover>
</template>

<style scoped>

</style>