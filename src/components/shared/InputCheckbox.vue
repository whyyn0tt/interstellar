<template>
  <div class="input-checkbox">
    <label :for="id" :class="{ checked: value }">
      <input type="checkbox" :id="id" :checked="value" @input="onInput" @change="onChange" />

      <span>
        <slot />
      </span>
    </label>
  </div>
</template>

<script>
export default {
  props: {
    id: {
      type: String,
      required: true,
    },

    value: {
      type: Boolean,
      default: false,
    },
  },

  emits: ['input', 'change'],

  methods: {
    onInput(event) {
      this.$emit('input', event.target.checked)
    },

    onChange(event) {
      this.$emit('change', event.target.checked)
    },
  },
}
</script>

<style lang="scss" scoped>
$color: $blue;

.input-checkbox {
  align-items: center;
  cursor: pointer;
  display: flex;

  @media (max-width: $tablet) {
    width: 100%;
  }

  &:hover input[type='checkbox'] {
    border-color: darken(white, 60%);
  }

  input[type='checkbox'] {
    $size: 18px;

    appearance: none;
    border: 2px solid $elevation-8-color;
    border-radius: $border-radius;
    color: white;
    cursor: pointer;
    height: $size;
    outline: 0;
    position: relative;
    transition: $transition;
    width: $size;
    flex-shrink: 0;

    &::before {
      $check-size: 8px;

      border-style: solid;
      border-color: white;
      border-width: 0 2px 2px 0;
      content: '';
      display: block;
      height: $check-size;
      left: calc(50% - #{calc($check-size / 2)});
      opacity: 0;
      position: absolute;
      top: 50%;
      transform: rotate(45deg) translate(-50%, -50%);
      width: calc($check-size / 2);
    }

    &:checked {
      background: $color;
      border-color: $color;
      color: white;

      &::before {
        opacity: 1;
      }
    }
  }

  label,
  input {
    cursor: pointer;
  }

  label {
    align-items: center;
    display: flex;
    font-size: 14px;

    @media (max-width: $tablet) {
      background: lighten($background-color, 2.5%);
      border: 2px solid lighten($background-color, 5%);
      border-radius: $border-radius;
      font-size: 18px;
      padding: 15px;
      transition: $transition;
      width: 100%;

      &.checked {
        background: rgba($color, 0.15);
        border-color: rgba($color, 0.5);
      }
    }

    span {
      margin-left: 5px;
    }
  }
}
</style>
