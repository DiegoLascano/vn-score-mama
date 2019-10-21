<template>
    <view>
        <nb-picker
            mode="dropdown"
            placeholder="Selecciona una opción"
            :style="{ backgroundColor: 'rgb(240, 240, 240)' }"
            :selectedValue="selected"
            :onValueChange="onValueChange">
            <item 
                v-for="state in dataArray"
                :key="state.value"
                :label="state.label" 
                :value="state.value" />
        </nb-picker>
    </view>
</template>

<script>
import { Picker } from "native-base";
export default {
    components: {
        Item: Picker.Item
    },
    props: ['array'],
    data() {
        return {
            dataArray: [],
            selected: ''
        }
    },
    mounted() {
        this.dataArray = this.array
    },
    methods: {
        onValueChange: function(value) {
            this.dataArray = this.dataArray.map(arrayElement => {
                if(arrayElement.value == value){
                    arrayElement.selected = true;
                    this.selected = value;
                }else{
                    arrayElement.selected = false
                }
                return arrayElement;
            });
        },
    },
}
</script>

<style>

</style>
