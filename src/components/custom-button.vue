<template>
  <component 
    :is="componentType"
    :href="href"
    :to="to"
    :class="['button', `button--${color}`,`button--${size}`, `button--${type}`, { 'is-block': block, 'is-disabled': disabled }]"
    :disabled="disabled"
    @click="handleClick"
  >
    <slot></slot>
  </component>
</template>

<script lang="ts">
import { defineComponent, computed } from 'vue';
import type { PropType } from 'vue';

export default defineComponent({
  name: 'CustomButton',
  props: {
    as: {
      type: String as PropType<'button' | 'a' | 'router-link'>,
      default: 'button'
    },
    href: {
      type: String,
      default: ''
    },
    to: {
      type: String,
      default: ''
    },
    size: {
      type: String as PropType<'small' | 'regular' | 'large'>,
      default: 'regular'
    },
    type: {
      type: String as PropType<'filled' | 'outlined'>,
      default: 'filled'
    },
    color: {
      type: String as PropType<'orange' | 'red' | 'orange-dark' | 'green' | 'green-dark'>,
      default: 'orange-dark'
    },
    block: Boolean,
    disabled: Boolean
  },
  setup(props, { emit }) {
    const componentType = computed(() => {
      switch (props.as) {
        case 'a': return 'a';
        case 'router-link': return 'router-link';
        default: return 'button';
      }
    });

    const isRouterLink = computed(() => {
      return props.as === 'router-link';
    });

    const handleClick = (event: Event) => {
      if (!props.disabled) {
        emit('click', event);
      }
    };

    return {
      componentType,
      handleClick
    };
  }
});
</script>

<style lang="scss" scoped>

.button {
  font-family: 'Montserrat';
  display: inline-flex;
  width: fit-content;
  margin: 5px;
  border: none;
  color: #fff;
  letter-spacing: -0.03em;
  text-align: center;
  cursor: pointer;
  text-decoration: none;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis; 

  &:hover {
    transition: .3s;
  }

  &:focus {
    outline: none;
    transition: .3s;
    box-shadow: 0 0 10px 5px rgba(0, 0, 0, 0.15);
  }

  &--small {
    font-family: 'Poppins';
    padding: 10px 16px;
    border-radius: 20px;
    font-size: 14px;
    line-height: 20px;
    font-weight: 500;
  }

  &--regular {
    padding: 14px 24px;
    border-radius: 24px;
    font-size: 16px;
    line-height: 20px;
    font-weight: 600;
  }

  &--large {
    padding: 16px 24px;
    border-radius: 28px;
    font-size: 18px;
    line-height: 24px;
    font-weight: 600;
  }

  &--orange-dark {
    background-color: #C2664E;
    &:hover {
      background-color: #DE8A74;
    }
  }

  &--orange {
    background-color: #FFBF52;
    &:hover {
      background-color: #FFD788;
    }
  }

  &--red {
    background-color: #F55555;
    &:hover {
      background-color: #FC6D6D;
    }
  }

  &--green {
    background-color: #30A47A;
    &:hover {
      background-color: #3DC696;
    }
  }

  &--green-dark {
    background-color: #113A29;
    &:hover {
      background-color: #235840;
    }
  }

  &--outlined {
    background-color: #fff;
    border: 1px solid #113A29;
    color: #113A29;
    &:hover {
      background-color: #DCF5EE;
      transition: .3s;
    }
  }

  &.is-block {
    display: block;
    width: 100%;
  }
  
  &.is-disabled {
    pointer-events: none;
    opacity: .4;
  }

  ::v-deep(img) {
    vertical-align: middle;
    max-width: 24px;
    max-height: 24px;
    height: auto;
  }

  ::v-deep(svg) {
    margin-right: 5px;
  }
}

</style>