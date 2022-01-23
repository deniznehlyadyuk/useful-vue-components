<template>
  <div id="app">
    <div id="filterContainer">
      <FilterBox
        ref="brands"
        v-model="selectedFilters.brands"
        :data-source="brands"
        :search-enabled="true"
        title="Marka"
        selection-mode="multiple"
      />
      <FilterBox
        ref="priceRanges"
        v-model="selectedFilters.priceRanges"
        :data-source="priceRanges"
        title="Fiyat Aralığı"
      />
    </div>
    <div style="width: 100%; background-color: lightyellow;">
      <SelectedFilterChips
        :data-source="allSelectedFilters"
        @unselect-filter="unselectFilter"
      />
    </div>
  </div>
</template>

<script>
import FilterBox from '../../../components/Examples/Filter/FilterBox'
import SelectedFilterChips from '../../../components/Examples/Filter/SelectedFilterChips'
export default {
  components: {
    FilterBox,
    SelectedFilterChips
  },
  data () {
    return {
      brands: [
        {
          id: 0,
          name: 'Apple'
        },
        {
          id: 1,
          name: 'Samsung'
        },
        {
          id: 2,
          name: 'Lenovo'
        },
        {
          id: 3,
          name: 'Huawei'
        },
        {
          id: 4,
          name: 'Xiaomi'
        },
        {
          id: 5,
          name: 'Asus'
        },
        {
          id: 6,
          name: 'Casper'
        },
        {
          id: 7,
          name: 'Microsoft'
        },
        {
          id: 8,
          name: 'TCL'
        },
        {
          id: 9,
          name: 'Hometech'
        },
        {
          id: 10,
          name: 'Everest'
        },
        {
          id: 11,
          name: 'Alcatel'
        },
        {
          id: 12,
          name: 'Concord'
        },
        {
          id: 13,
          name: 'Reeder'
        },
        {
          id: 14,
          name: 'Philips'
        },
        {
          id: 15,
          name: 'Rockchip'
        },
        {
          id: 16,
          name: 'Vorcom'
        },
        {
          id: 17,
          name: 'Ixtech'
        },
        {
          id: 18,
          name: 'Hegitech'
        },
        {
          id: 19,
          name: 'Technopc'
        },
        {
          id: 20,
          name: 'Redline'
        },
        {
          id: 21,
          name: 'Techstorm'
        },
        {
          id: 22,
          name: 'Teclast'
        },
        {
          id: 23,
          name: 'Elephone'
        },
        {
          id: 24,
          name: 'Jedi'
        },
        {
          id: 25,
          name: 'TenPlus'
        },
        {
          id: 26,
          name: 'Vestel'
        },
        {
          id: 27,
          name: 'Alldocube'
        },
        {
          id: 28,
          name: 'Chuwi'
        },
        {
          id: 29,
          name: 'Exper'
        },
        {
          id: 30,
          name: 'Fluo'
        },
        {
          id: 31,
          name: 'Goldmaster'
        },
        {
          id: 32,
          name: 'NPO'
        },
        {
          id: 33,
          name: 'Piranha'
        },
        {
          id: 34,
          name: 'Pritom'
        },
        {
          id: 35,
          name: 'Spreadtrum'
        },
        {
          id: 36,
          name: 'Sunny'
        },
        {
          id: 37,
          name: 'Vankyo'
        },
        {
          id: 38,
          name: 'Wenn'
        },
        {
          id: 39,
          name: 'Yeamuds'
        },
        {
          id: 40,
          name: 'Amazon'
        },
        {
          id: 41,
          name: 'Denver'
        },
        {
          id: 42,
          name: 'Dragon Touch'
        },
        {
          id: 43,
          name: 'Enthalpy'
        },
        {
          id: 44,
          name: 'Fusion'
        },
        {
          id: 45,
          name: 'General Mobile'
        },
        {
          id: 46,
          name: 'Gigaset'
        },
        {
          id: 47,
          name: 'Google'
        },
        {
          id: 48,
          name: 'Insignia'
        },
        {
          id: 49,
          name: 'Newland'
        },
        {
          id: 50,
          name: 'Osmart'
        },
        {
          id: 51,
          name: 'Rca'
        },
        {
          id: 52,
          name: 'Redway'
        },
        {
          id: 53,
          name: 'Regal'
        },
        {
          id: 54,
          name: 'Smarttab'
        },
        {
          id: 55,
          name: 'Soultech'
        },
        {
          id: 56,
          name: 'Stormax'
        },
        {
          id: 57,
          name: 'Turkcell'
        },
        {
          id: 58,
          name: 'Ultrapad'
        },
        {
          id: 59,
          name: 'Vastking'
        }
      ],
      priceRanges: [
        {
          id: 1,
          name: '250-500 TL',
          value: {
            min: 250,
            max: 500
          }
        },
        {
          id: 2,
          name: '500-750 TL',
          value: {
            min: 500,
            max: 750
          }
        },
        {
          id: 3,
          name: '750-1000 TL',
          value: {
            min: 750,
            max: 1000
          }
        }
      ],
      selectedFilters: {
        brands: [],
        priceRanges: null
      }
    }
  },
  computed: {
    allSelectedFilters () {
      const list = []
      for (const filterType in this.selectedFilters) {
        if (this.selectedFilters[filterType] == null) {
          continue
        }

        const element = JSON.parse(JSON.stringify(this.selectedFilters[filterType]))

        const isArray = Array.isArray(element)
        if (!isArray) {
          element.category = filterType
          list.push(element)
          continue
        }

        element.forEach((e) => {
          e.category = filterType
          list.push(e)
        })
      }
      return list
    }
  },
  methods: {
    unselectFilter (filter) {
      const object = this.selectedFilters[filter.category]
      if (Array.isArray(object)) {
        const index = object.findIndex(e => e.id === filter.id)
        object.splice(index, 1)
      } else {
        this.selectedFilters[filter.category] = null
      }
      this.$refs[filter.category].unselectItem(filter.id)
    }
  }
}
</script>

<style scoped>
#app {
  display: flex;
}
#filterContainer {
  display: flex;
  flex-direction: column;
}
</style>
