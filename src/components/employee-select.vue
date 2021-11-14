<template>
  <div class="v-select">
    <div
      class="v-select-selected"
      :class="{ active: optionsOpened == true  }"
      @click="optionsToggle"
    >
      <div class="v-select-selected-placeholder">
        <img
          class="v-select-selected-img"
          :src="selected.img"
          alt="image"
        >
      </div>
      <div class="v-select-selected-name">
        {{ selected.name }}
      </div>
      <span class="v-select-selected-icon"></span>
    </div>
    <div
      class="v-select-options"
      v-show="optionsOpened == true"
    >
      <div
        class="v-select-option"
        v-for="user in users"
        :key="user.id"
        @click="selectOption(user)"
      >
        <div class="v-select-option-placeholder">
          <img
            class="v-select-option-img"
            :src="user.img"
            alt="image"
          >
        </div>
        <div class="v-select-option-name">
          {{ user.name }}
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    users: {
      type: Array,
      required: true
    }
  },
  data () {
    return {
      selected: '',
      optionsOpened: false
    }
  },
  methods: {
    optionsToggle () {
      this.optionsOpened = !this.optionsOpened
    },
    selectOption (user) {
      this.selected = user
      this.optionsOpened = false
    }
  },
  mounted () {
    this.selected = this.users[0]
  }
}
</script>

<style lang="scss">
:root {
  --gray-border: rgba(0, 66, 105, 0.28);
}

.v-select {
  &-selected {
    // padding: 0.5rem 1.06rem;
    padding: 0.5rem 3.6rem 0.5rem 1.06rem;
    position: relative;
    min-height: 2.94rem;
    border: 1px solid var(--gray-border);
    border-radius: 0.44rem;
    background: #fff;
    cursor: pointer;

    text-overflow: ellipsis;

    &.active {
      border-bottom: 0;
      border-bottom-right-radius: 0;
      border-bottom-left-radius: 0;
    }

    &-icon {
      position: relative;
      display: block;
      position: absolute;
      top: 50%;
      right: 5%;
      transform: translateY(-50%);
      width: 0.5rem;
      height: 0.28rem;
      background: url("../assets/img/icons/select-arrow.svg") 0 0 / cover
        no-repeat;
    }
    &-name {
      // padding-right: 1rem;
      text-overflow: ellipsis;
    }
  }

  &-selected-img,
  &-option-img {
    display: block;
    width: 100%;
    max-width: 100%;
    object-fit: cover;
    border-radius: 100%;
  }

  &-selected-placeholder,
  &-option-placeholder {
    margin-right: 0.75rem;
    width: 2rem;
    border-radius: 100%;
  }

  &-selected,
  &-option {
    display: flex;
    align-items: center;
  }

  &-options {
    padding: 1rem 0;
    border: 1px solid var(--gray-border);
    border-bottom-left-radius: 0.44rem;
    border-bottom-right-radius: 0.44rem;
    background: #fff;
  }
  &-option {
    padding: 0.5rem 1.06rem;
    cursor: pointer;

    &:not(:last-child) {
      margin-bottom: 1rem;
    }
  }
}
</style>
