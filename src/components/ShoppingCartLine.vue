<template>
        <tr>
            <td> 
                <!-- <v-text-field type="number" v-bind:value="qvalue" v-on:input="sendChangeEvent"></v-text-field>  -->
                <input type="number"   style="width:5em"
                v-bind:value="qvalue"
                v-on:input="sendChangeEvent"/>
            </td>
            <td>{{ line.product.name }}</td>
            <td>{{ line.product.price | currency }}</td>
            <td> {{ (line.quantity * line.product.price) | currency }}</td>
            <td>
                <v-btn small color="red white--text" @click="sendRemoveEvent">Remove</v-btn>
            </td>
        </tr>
</template>

<script>
    export default {
    name: "ShoppingCartLine",
    props: ['line'],
    data: function() {
            return {
                qvalue: this.line.quantity
            }
    },
    methods: {
        sendChangeEvent($event) {
            if ($event.target.value > 0) {
                this.$emit("quantity", Number($event.target.value));
                this.qvalue = $event.target.value;
            } else {
                this.$emit("quantity", 1);
                this.qvalue = 1;
                $event.target.value = this.qvalue;
            }
        },
        sendRemoveEvent() {
            this.$emit("remove", this.line);
        }
    }
  }
</script>

<style lang="scss" scoped>

</style>