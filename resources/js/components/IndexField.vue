<template>
    <div>
        <popper hover :content="getTooltip()">
            <Icon :type="this.field.solid_icon ? 'solid' : 'outline'" :name="getValue()" :class="getColor()" />
        </popper>
    </div>
</template>

<script>
import Icon from './Icon.vue';

export default {
    props: ['resourceName', 'field'],
    components: {
        Icon,
    },
    methods: {
        getValue: function() {
            if (!this.field.values) return this.field.value;
            return Object.keys(this.field.values).filter(val => this.field.values[val])[0];
        },
        getTooltip: function() {
            if (this.field.tooltip) {
                if (typeof this.field.tooltip == "string") return this.field.tooltip;
                else return this.field.tooltip[this.getValue()];
            }
        },
        getColor: function() {
            if (this.field.color) {
                if (typeof this.field.color == "string") return 'text-' + this.field.color;
                else return 'text-' + this.field.color[this.getValue()];
            }
        },
    }
}
</script>
