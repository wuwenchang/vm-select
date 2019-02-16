<template>
  <div class="vm-select"
    ref="vmselect"
    :class="vmClass"
    v-click-outside.capture="onClickOutside"
    v-click-outside:mousedown.capture="onClickOutside">
    <div class="vm-select-section" @click="openDropdown">
      <div class="vm-select--label" v-if="displayLabel">{{displayLabel}}</div>
      <div class="vm-select--label vm-select--placeholder" v-else>{{defaultStrings.placeholder}}</div>
      <i class="vm-select--icon-arrow"></i>
    </div>
    <transition name="vm-drop">
      <div class="vm-select-dropdown" v-show="visible">
        <input type="text"
          ref="searchText"
          class="vm-select--input"
          autocomplete="off"
          :placeholder="defaultStrings.search"
          v-if="search"
          v-model="keywords"/>
        <div class="vm-select--actionbox" v-if="multiple">
          <button type="button" class="vm-actionbox" @click="actionbox('all')">{{ defaultStrings.actionAll }}</button>
          <button type="button" class="vm-actionbox" @click="actionbox('cancel')">{{ defaultStrings.actionNone }}</button>
        </div>
        <ul class="vm-dropdown--content">
          <li :class="optionHighlight(option, index)" v-for="(option, index) in filterOptions" :key="index" @click.stop="selectOption(option, index)">
            <div class="vm-dropdown--element">
              <slot name="option" :option="option">
                {{getOptionLabel(option)}}
              </slot>
            </div>
          </li>
          <li v-if="filterOptions.length == 0">
            <div class="vm-dropdown--element element--empty">{{defaultStrings.empty}}</div>
          </li>
        </ul>
      </div>
    </transition>
  </div>
</template>
<script>
import { directive as clickOutside } from 'v-click-outside-x'
import isEmpty from 'is-empty'
export default {
  name: 'vm-select',
  components: {},
  props: {
    value: {
      type: [Array, String, Number]
    },
    options: {
      type: Array,
      default: () => []
    },
    multiple: {
      type: Boolean,
      default: false
    },
    search: {
      type: Boolean,
      default: false
    },
    disabled: {
      type: Boolean,
      default: false
    },
    label: {
      type: String
    },
    labelKey: {
      type: String
    },
    labelDisabled: {
      type: [String, Function]
    },
    customLabel: {
      type: Function,
      default (option, label) {
        if (isEmpty(option)) return ''
        return label ? option[label] : option
      }
    },
    customDisabled: {
      type: Function,
      default: () => { return false }
    },
    strings: {
      type: Object,
      default: () => {}
    }
  },
  directives: { clickOutside },
  data () {
    return {
      visible: false,
      keywords: null,
      defaultStrings: {
        placeholder: '请选择...',
        search: '请输入查询条件...',
        countSelected: '已选中{0}项',
        empty: '无搜索匹配项',
        actionAll: '全选',
        actionNone: '全不选'
      }
    }
  },
  computed: {
    newValue () {
      if (isEmpty(this.value)) {
        return this.multiple ? [] : ''
      } else {
        return this.value
      }
    },
    vmClass () {
      return {
        'active': this.visible,
        'disabled': this.disabled
      }
    },
    optionsType () {
      if (this.options.length > 0) {
        if (typeof this.options[0] === 'object') {
          return true // 数组对象
        }
      }
      return false // 单数组
    },
    filterOptions () {
      let keyword = this.keywords
      if (keyword) {
        let result = this.options.filter(option => this.optionsTypeValue(option).toLowerCase().indexOf(keyword.toLowerCase()) !== -1)
        return result
      } else {
        return this.deepCopy(this.options)
      }
    },
    selectedItems () {
      let result = null
      let v = this.value || this.newValue
      if (!isEmpty(this.newValue)) {
        if (this.optionsType) {
          if (this.multiple) {
            result = this.deepCopy(this.options).filter(o => v.some(v => v === o[this.labelKey]))
          } else {
            result = this.deepCopy(this.options).find(o => o[this.labelKey] === v)
          }
        } else {
          result = v
        }
      }
      return result
    },
    displayLabel () {
      // 提示传参是否匹配
      if (this.optionsType && (!this.label || !this.labelKey)) {
        throw new Error('[vm-select warn]: When `:options` is an array of objects, Must be "label" and "labelKey" attributes')
      }
      if (this.multiple && !Array.isArray(this.value)) {
        throw new Error('[vm-select warn]: v-model must be Array when multiple is true')
      }
      if (!this.multiple && Array.isArray(this.value)) {
        throw new Error('[vm-select warn]: v-model must be String or Number when multiple is false')
      }
      let txt = ''
      if (this.multiple) {
        if (this.value.length > 1) {
          txt = this.defaultStrings.countSelected.replace('{0}', this.value.length)
        } else if (this.value.length === 1) {
          txt = this.optionsType ? this.selectedItems[0][this.label] : this.selectedItems[0]
        }
      } else {
        let isCustomLabel = this.customLabel(this.selectedItems, this.label)
        if (!isEmpty(isCustomLabel)) {
          txt = isCustomLabel
        } else {
          txt = this.optionsType ? this.selectedItems[this.label] : this.value
        }
      }
      return txt
    }
  },
  mounted () {
    console.log(this.value)
    this.defaultStrings = Object.assign(this.defaultStrings, this.strings)
  },
  methods: {
    optionsTypeValue (option) {
      return this.optionsType ? option[this.label] : option
    },
    onClickOutside () {
      this.visible = false
    },
    openDropdown () {
      this.visible = !this.visible
      if (!this.visible) return
      // keep the query for remote select
      this.keywords = null
      const bottomDistance = document.documentElement.clientHeight - this.$el.getBoundingClientRect().bottom
      const boxHeight = this.$el.offsetHeight + 1
      this.$nextTick(() => {
        const dropdownHeight = this.$el.children[1].offsetHeight
        if (bottomDistance < dropdownHeight) {
          this.$el.children[1].style.bottom = boxHeight + 'px'
          this.$el.children[1].style.transformOrigin = 'center bottom 0px'
        } else {
          this.$el.children[1].setAttribute('style', '')
        }
      })
    },
    getOptionLabel (option) {
      let isCustomLabel = this.customLabel(option, this.label)
      if (!isEmpty(isCustomLabel)) {
        return isCustomLabel
      }
      return this.optionsType ? option[this.label] : option
    },
    actionbox (type) {
      let result = []
      if (type === 'all') {
        this.filterOptions.map(option => {
          // 过滤掉 disabled 项
          if (!this.customDisabled(option)) {
            let v = this.optionsType ? option[this.labelKey] : option
            if (this.value.indexOf(v) === -1) {
              this.value.push(v)
            }
          }
        })
      } else {
        this.filterOptions.map(option => {
          // 过滤掉 disabled 项
          if (!this.customDisabled(option)) {
            let v = this.optionsType ? option[this.labelKey] : option
            let findIndex = this.value.indexOf(v)
            if (findIndex !== -1) {
              this.value.splice(findIndex, 1)
            }
          }
        })
      }
      result = this.value
      this.$emit('input', result)
      this.$emit('on-change', result)
    },
    selectOption (option, key) {
      let curValue = this.optionsType ? option[this.labelKey] : option
      if (this.multiple) {
        // 如当前已选中，需反选
        let curIndex = this.value.findIndex(v => v === curValue)
        if (curIndex > -1) {
          this.value.splice(curIndex, 1)
        } else {
          this.value.push(curValue)
        }
        this.$emit('input', this.value)
        this.$emit('on-change', curValue)
      } else {
        this.visible = false
        this.$emit('input', curValue)
        this.$emit('on-change', curValue)
      }
    },
    optionLabelKey (option) {
      return this.optionsType ? option[this.labelKey] : option
    },
    optionHighlight (option, index) {
      let result = false
      let optionValue = this.optionsType ? option[this.labelKey] : option
      if (this.multiple) {
        result = this.value.some(v => v === optionValue)
      } else {
        result = this.value ? this.value === optionValue : false
      }
      return {
        'multiple--selected': this.multiple && result,
        'single--selected': !this.multiple && result,
        'disabled--selected': this.customDisabled(option)
      }
    },
    deepCopy (source) {
      let sourceCopy = source instanceof Array ? [] : {}
      for (let item in source) {
        sourceCopy[item] = typeof source[item] === 'object' ? this.deepCopy(source[item]) : source[item]
      }
      return sourceCopy
    }
  }
}
</script>
<style src="./index.less" lang="less"></style>
