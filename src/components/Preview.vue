<template>
  <div class="preview">
    <div v-if="parent.name.length > 0" class="preview-parent">
      <h3>Персональные данные</h3>
      <div class="preview-parent__info">
        {{ parent.name }}, {{ parent.age }}
      </div>
    </div>
    <div v-if="children.length > 0" class="preview-children">
      <h3>Дети</h3>
      <div v-for="(child, index) in children" :key="index" class="preview-children__info">
        {{child.name }}, {{ child.age }}
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    name: "site-preview",
    props: ['parent', 'children'],
  }
</script>