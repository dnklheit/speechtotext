<template>
  <div class="note_item">
    <div class="id_content">
      <span> #{{ noteItem.id }} </span>
    </div>
    <div class="note_content">
      {{ noteItem.note }}
            <br/>

      <br/>
       <small>Oluşturulma tarihi: {{ noteItem.timestamp }}</small>
    </div>
    
  </div>
</template>

<script>
export default {
  props: {
    noteItem: {
      type: Object,
      required: true,
    },
  },
};
</script>
