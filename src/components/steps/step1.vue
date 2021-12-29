<template>
    <div class="mb-3">
        <label for="NameFormControlInput1" class="form-label">שם מלא</label>
        <input type="text" class="form-control" id="NameFormControlInput1" :value="name" @input="updateName" placeholder="שם מלא">
    </div>
</template>

<script>
    export default {
      name: "step1",
      props: {
        name: String
      },
      emits: [
          'update:name'
      ],
      methods: {
        updateName (e) {
          this.$emit('update:name', e.target.value)
        }
      }
    }

</script>

<style scoped>

</style>
