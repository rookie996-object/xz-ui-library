<template>
    <div class="tabs-head" ref="head">
        <slot></slot>
        <div class="line" ref="line"></div>
        <div class="actions-wrapper">
            <slot name="actions"></slot>
        </div>
    </div>
</template>

<script>
    export default {
        name: 'XZTabsHead',
        inject: ['eventBus'],
        mounted() {
            this.eventBus.$on('update:selected', (item, vm) => {
                let {width, left} = vm.$el.getBoundingClientRect()
                let headLeft =  this.$refs.head.getBoundingClientRect().left
                this.$refs.line.style.width = `${width}px`
                this.$refs.line.style.left = `${left - headLeft}px`
            })
        }
    }
</script>

<style lang="scss" scoped>
$tab-height: 40px;
$line-color: blue;
$border-color: #ddd;
.tabs-head {
    position: relative;
    display: flex;
    height: $tab-height;
    align-items: center;
    justify-content: flex-start;
    border-bottom: 1px solid $border-color;
    > .line {
      position: absolute;
      bottom: 0;
      border-bottom: 1px solid $line-color;  
      transition: all .5s ;
    }
    > .actions-wrapper {
        display: flex;
        justify-content: center;
        align-items: center;
        margin-left: auto;
        padding: 0 1em;
    }
}
</style>