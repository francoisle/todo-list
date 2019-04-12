<template>
  <div :class="{ highLight }" class="item-container">
    <div class="item-container__item checkbox">
      <input :id="itemId" @click="handleItemClick(item.id)" type="checkbox" />
      <label
        :class="{ checked: item.state === 'DONE' }"
        :for="itemId"
        class="item-container__item__item-text"
        >{{ item.title }}</label
      >
    </div>
    <button :disabled="item.state !== 'TODO'" @click="handleHighLight(item.id)">
      {{ highLight ? "Unhighlight !" : "Highlight !" }}
    </button>
  </div>
</template>

<script>
export default {
  name: "TodoItem",
  props: ["item", "highLight", "handleItemClick", "handleHighLight"],
  computed: {
    itemId() {
      return "item-" + this.item.id;
    }
  }
};
</script>

<style scoped>
.item-container {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  margin-bottom: 15px;
}

.item-container.highLight {
  background-color: lightskyblue;
}

.item-container__item__item-text.checked {
  text-decoration: line-through;
  font-style: italic;
}

/* Hide native checkbox */
.checkbox input[type="checkbox"] {
  opacity: 0;
}

.checkbox label {
  user-select: none;
  position: relative;
  display: inline-block;
  padding-left: 30px;
}

.checkbox label::before,
.checkbox label::after {
  position: absolute;
  content: "";
  display: inline-block;
}

/* Outer-box */
.checkbox label::before {
  content: "";
  display: inline-block;
  height: 16px;
  width: 16px;
  border: 1px solid;

  left: 0;
  top: 3px;
}

/* Check mark */
.checkbox label::after {
  content: "";
  display: inline-block;
  height: 6px;
  width: 9px;
  border-left: 2px solid;
  border-bottom: 2px solid;
  transform: rotate(-45deg);

  left: 4px;
  top: 7px;
}

/* Hide te check mark by default */
.checkbox input[type="checkbox"] + label::after {
  content: none;
}

/* Un hide the check mark on the checked state */
.checkbox input[type="checkbox"]:checked + label::after {
  content: "";
}

/* Adding focus styles on the outer-box of the fake checkbox */
.checkbox input[type="checkbox"]:focus + label::before {
  outline: rgb(59, 153, 252) auto 5px;
}
</style>
