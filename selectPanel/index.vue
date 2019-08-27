<template>
  <div class="cas-select-panel">
    <div class="cas-select-panel__header">
      <div class="cas-select-panel__title">{{title}}</div>
      <div class="cas-select-panel__clear"
           @click="handleClearAll">清空全部</div>
    </div>
    <div class="cas-select-panel__content">
      <div class="cas-select-panel__item"
           v-for="item in data"
           :key="item.id">
        <span class="cas-select-panel__item-text">{{item[setting.label]}}</span>
        <span class="cas-select-panel__item-remove"
              v-if="!item.disabled"
              @click="handleRemove(item.id)">x</span>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  name: 'CasSelectPanel',
  props: {
    data: {
      type: Array
    },
    title: {
      type: String,
      default: '已选'
    },
    setting: {
      default: function () {
        return {
          label: 'text',
          key: 'id'
        };
      }
    }
  },
  methods: {
    handleClearAll() {
      this.$emit('clear-all', this.data.map(item => {
        if (!item.disabled) {
          return item.id
        }
      }));
    },
    handleRemove(id) {
      this.$emit('remove', id);
    }
  }
};
</script>
<style lang="less" scoped>
@prefix: cas-select-panel;
.@{prefix} {
  background-color: #fff;
  border: 1px solid #dee4f5;
  border-radius: 2px;
}

.@{prefix}__header {
  display: flex;
  justify-content: space-between;
  font-family: PingFangSC-Medium;
  color: #1c2438;
  letter-spacing: 0;
  border-bottom: 1px solid #dee4f5;
  background-color: #fafbfe;
  font-size: 14px;
  padding: 0 12px;
  line-height: 36px;
}

.@{prefix}__clear {
  color: blue;
  cursor: pointer;
}

.@{prefix}__content {
  padding: 10px;
}

.@{prefix}__item {
  display: flex;
  justify-content: space-between;
  padding: 5px;
  background: #f8f8f8;
  cursor: pointer;
  margin: 10px 0;
}
.@{prefix}__item-remove {
  cursor: pointer;
}
</style>
