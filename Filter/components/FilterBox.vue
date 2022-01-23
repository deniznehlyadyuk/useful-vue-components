<template>
  <div id="filterApp">
    <div class="header">
      <div class="title">
        {{ title }}
      </div>
      <DxButton
        type="danger"
        icon="minus"
        :on-click="unselectAll"
      />
    </div>
    <DxList
      ref="list"
      :data-source="modifiedDataSource"
      :selection-mode="selectionMode"
      :show-selection-controls="true"
      :search-enabled="searchEnabled"
      :on-selection-changed="updateSelectedItems"
      key-expr="id"
      display-expr="name"
      search-expr="name"
    >
      <DxSearchEditorOptions
        placeholder="Filtrele"
        styling-mode="underlined"
        :hover-state-enabled="false"
        :focus-state-enabled="false"
      />
    </DxList>
  </div>
</template>

<script>
import { DxButton } from 'devextreme-vue/button'
import { DxList, DxSearchEditorOptions } from 'devextreme-vue/list'
import DataSource from 'devextreme/data/data_source'
export default {
  components: {
    DxButton,
    DxList,
    DxSearchEditorOptions
  },
  props: {
    title: {
      type: String,
      required: true
    },
    dataSource: {
      type: Array,
      required: true
    },
    selectionMode: {
      type: String,
      default: 'single'
    },
    searchEnabled: {
      type: Boolean,
      default: false
    }
  },
  data () {
    return {
      selectedItems: []
    }
  },
  computed: {
    list () {
      return this.$refs.list.instance
    },
    modifiedDataSource () {
      return new DataSource({
        store: this.dataSource,
        pageSize: this.dataSource.length
      })
    }
  },
  watch: {
    selectedItems () {
      if (this.selectionMode !== 'multiple') {
        this.$emit('input', this.selectedItems[0])
        return
      }
      this.$emit('input', this.selectedItems)
    }
  },
  methods: {
    updateSelectedItems (e) {
      e.addedItems.forEach((x) => {
        this.selectedItems.push(x)
      })
      e.removedItems.forEach((x) => {
        const index = this.selectedItems.indexOf(x)
        if (index !== -1) {
          this.selectedItems.splice(index, 1)
        }
      })
    },
    unselectAll () {
      if (this.searchEnabled) {
        this.list.option('searchValue', '')
      }
      this.selectedItems = []
      this.list.unselectAll()
    },
    unselectItem (id) {
      const item = this.dataSource.find(e => e.id === id)
      this.list.unselectItem(item)
    }
  }
}
</script>

<style scoped>
#filterApp {
  display: flex;
  flex-direction: column;
  max-height: 350px;
  width: 225px;
  border: 1px solid #DDDDDD;
  padding: 5px;
  margin: 0 5px 5px 0;
}
#filterApp .title {
  margin-bottom: 10px;
}
.header {
  position: relative;
  display: flex;
  justify-content: space-between;
}
.header .dx-button {
  position: absolute;
  right: 0;
}
.header >>> .dx-icon {
  vertical-align: baseline !important;
}
</style>
