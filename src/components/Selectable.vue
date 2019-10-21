<template>
    <view class="flex-container">
        <nb-button
            class="flex-item"
            v-for="data in dataArray"
            :key="data.id"
            @press="onItemSelected(data.id)" 
            :bordered="!data.selected"
            primary>
            <nb-text :style="{ textAlign: 'center' }">{{ data.text }}</nb-text>
        </nb-button>
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
        flex-wrap: wrap;
        justify-content: space-between;
        align-items: center;
    }
    .flex-item{
        width: 26%;
        margin: 10px;
        padding: 10px;
    }
</style>
