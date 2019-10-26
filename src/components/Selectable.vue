<template>
    <view class="flex-container">
        <!-- <nb-button
            class="flex-item"
            v-for="data in dataArray"
            :key="data.id"
            @press="onItemSelected(data.id)" 
            :bordered="!data.selected"
            primary>
            <nb-text class="options">{{ data.text }}</nb-text>
        </nb-button> -->
        <text
            v-for="data in dataArray"
            :key="data.id"
            :class="{ 'options': true , 'selected': data.selected }"
            @press="onItemSelected(data.id)">
            {{ data.text }}
        </text>
    </view>
</template>

<script>
export default {
    props: ['array'],
    data() {
        return {
            dataArray: []
        }
    },
    mounted() {
        this.dataArray = this.array
    },
    methods: {
        onItemSelected(id) {
            this.dataArray = this.dataArray.map( arrayElement => {
                if(arrayElement.id == id){
                    arrayElement.selected = true;
                    // arrayElement.color = 'green'
                }else{
                    arrayElement.selected = false;
                    // arrayElement.color = 'grey'
                }
                return arrayElement
            })
        }
    },
}
</script>

<style>
    .flex-container{
        flex-direction: row;
        /* flex-wrap: wrap; */
        justify-content: flex-start;
        /* align-items: center; */
        /* background-color: rgb(240, 240, 240); */
        /* margin-left: 10px; */
    }
    .options{
        flex: 1;
        font-size: 14px;
        border-width: 1px;
        /* background-color: lightslategray;
        color: aqua; */
        border-color: rgb(199, 199, 204);
        padding-top: 8px;
        padding-bottom: 8px;
        text-align: center;
        /* color: rgb(72, 72, 74); */
    }
    .selected{
        background-color: #007bff;
        color: white;
    }
</style>
