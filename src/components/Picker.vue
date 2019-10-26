<template>
    <view>
            <!-- :style="{ backgroundColor: 'rgb(242,242,247)' }" -->
                <!-- backgroundColor: '#d3d3d3', -->
        <nb-picker
            mode="dropdown"
            placeholder="Selecciona una opción"
            iosHeader="Seleccionar"
            :textStyle="{ color: '#007bff', fontSize: 14 }"
            :itemStyle="{
                marginLeft: 0,
                paddingLeft: 20
            }"
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
