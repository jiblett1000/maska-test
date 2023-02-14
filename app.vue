<template>
  <div>
    <CustomInput
      name="phone"
      type="tel"
      label="Phone number"
      autocomplete="on"
      placeholder="e.g. xxx-xxx-xxx"
      :value="'6666666666'"
      :mask-options="{
        mask: '+1 (###) ###-####',
        eager: true,
      }"
    >
    </CustomInput>
  </div>
</template>

<script setup lang="ts"></script>

<style>
body {
  background-color: antiquewhite;
}
.theInput {
  background-color: antiquewhite;
  width: 10rem;
  padding: 1rem 1rem;
  font-size: 1rem;
  border-radius: 0.75rem;
  border-style: solid;
  border-color: #999;
}
</style>
