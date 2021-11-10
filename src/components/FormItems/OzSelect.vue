<template>
  <div class="oz-select" v-click-outside="hideDropdown">
    <oz-input v-bind="$attrs" @focus="isDropdownOpen = true" :value="value"/>
    <div v-if="isDropdownOpen" class="oz-select-selector__dropdown">
      <ul v-if="items.length" class="oz-select-selector__dropdown-items">
        <li v-for="item in items" :key="item.id" :class="getItemClasses(item)" @click="selectItem(item)">
          {{ item[name] }}
        </li>
      </ul>
      <div
        v-else
        class="empty"
      >
        Ничего не найдено
      </div>
    </div>
  </div>
</template>

<script>
import OzInput from './OzInput.vue';
import ClickOutside from "vue-click-outside";

export default {
  components: { OzInput },
  model: {
    prop: "value",
    event: "input",
  },
  directives: {
    ClickOutside,
  },
  props: {
    value: {
      type: String,
      default: () => {},
    },
    items: {
      type: Array,
    },
    name: {
      type: String,
    },
  },

  data() {
    return {
      isDropdownOpen: false,
    };
  },

  methods: {
    hideDropdown() {
      this.isDropdownOpen = false
    },

    selectItem (item) {
      const { name } = this

      this.$emit("input", item[name]);
      this.hideDropdown();
    },

    isCheckedItem (item) {
      const { value, name } = this;

      return item[name] === value;
    },

    getItemClasses (item) {
      return [
        'oz-select-selector__dropdown-item',
        this.isCheckedItem(item) && 'oz-select-selector__dropdown-item-active'
      ];
    },
  },
};
</script>

<style>
.oz-select {
  flex: 1;
  position: relative;
}

.oz-select-selector__dropdown {
  position: absolute;
  top: calc(100% - 8px);
  left: 0;
  z-index: 1;
  box-sizing: border-box;
  width: 100%;
  background-color: #BBB;
  border-color: #0CC;
  border-style: solid;
  border-width: 1px;
  border-top: none;
}

.oz-select-selector__dropdown-items {
  box-sizing: border-box;
  width: 100%;
  max-height: 256px;
  margin: 0;
  padding: 0;
  overflow-x: hidden;
  overflow-y: auto;
  list-style: none;
}

.oz-select-selector__dropdown-item {
  display: block;
  box-sizing: border-box;
  padding: 6px 20px 6px 20px;
  color: var(--s-select-list-item-color-text);
  font-size: 14px;
  line-height: 18px;
  cursor: pointer;
  user-select: none;
}
.oz-select-selector__dropdown-item:hover {
  background-color: #e4d299a4;
}
.oz-select-selector__dropdown-item-active {
  background-color: #e9c13ca4;
}
</style>
