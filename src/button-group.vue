<template>
    <div class="z-button-group">
        <slot></slot>
    </div>
</template>

<script>
    export default {
        mounted() {
            for(let node of this.$el.children) {
                let name = node.nodeName.toLowerCase()
                if(name !== 'button') {
                    console.warn(`Child elements of g-button-group should be all g-buttons，But you use was ${name}`)
                }
            }
        }
    }
</script>

<style lang="scss" scoped>
$border-radius: 4px;
.z-button-group {
    display: inline-flex;
    vertical-align: middle;
    > .z-button {
        border-radius: 0;
        &:not(:first-child) {
            margin-left: -1px;
        }
        &:first-child {
            border-top-left-radius: $border-radius;
            border-bottom-left-radius: $border-radius;
        }
        &:last-child {
            border-top-right-radius: $border-radius;
            border-bottom-right-radius: $border-radius;
        }
        &:hover {
            position: relative;
            z-index: 1;
        }
    }
}
</style>