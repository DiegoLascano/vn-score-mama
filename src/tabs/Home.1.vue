<template>
    <nb-content>
        <view class="score-result" :style="{ backgroundColor: scoreColor }">
            <text>
                Score:
            </text> 
            <text>
                {{ scoreMAMA }}
            </text>
        </view>
        <view>
            <text :style="{ padding: 10 }">
                Selecione la frecuencia cardiaca
            </text>
            <view class="flex-container">
                <touchable-opacity 
                    class="flex-item"
                    v-for="fc in fcRanges"
                    :key="fc.id"
                    @press="onItemSelected(fcRanges, fc.id)" 
                    :style="{ backgroundColor: fc.color}">
                    <text :style="{ textAlign: 'center' }">{{ fc.text }}</text>
                </touchable-opacity>
            </view>
        </view>
        <view>
            <text :style="{ padding: 10 }">
                Seleccione la presión Sistólica
            </text>
            <view class="flex-container">
                <touchable-opacity 
                    class="flex-item"
                    v-for="sistolica in sistRanges"
                    :key="sistolica.id"
                    @press="onItemSelected(sistRanges, sistolica.id)" 
                    :style="{ backgroundColor: sistolica.color}">
                    <text :style="{ textAlign: 'center' }">{{ sistolica.text }}</text>
                </touchable-opacity>
            </view>
        </view>
        <view>
            <text :style="{ padding: 10 }">
                Seleccione la presión Diastólica
            </text>
            <view class="flex-container">
                <touchable-opacity 
                    class="flex-item"
                    v-for="diastolica in diastRanges"
                    :key="diastolica.id"
                    @press="onItemSelected(diastRanges, diastolica.id)" 
                    :style="{ backgroundColor: diastolica.color}">
                    <text :style="{ textAlign: 'center' }">{{ diastolica.text }}</text>
                </touchable-opacity>
            </view>
        </view>
        <view>
            <text :style="{ padding: 10 }">
                Seleccione la frecuencia respiratoria
            </text>
            <view class="flex-container">
                <touchable-opacity 
                    class="flex-item"
                    v-for="fr in frRanges"
                    :key="fr.id"
                    @press="onItemSelected(frRanges, fr.id)" 
                    :style="{ backgroundColor: fr.color}">
                    <text :style="{ textAlign: 'center' }">{{ fr.text }}</text>
                </touchable-opacity>
            </view>
        </view>
        <!-- <text>
            {{ fcRanges }}
        </text> -->
    </nb-content>
</template>

<script>
export default {
    props: {
        navigation: {
            type: Object
        },
    },
    data() {
        return {
            fcRanges: [
                { id: 0, text: '<=50', score: 3, selected: false, color: 'grey' },
                { id: 1, text: '51-59', score: 1, selected: false, color: 'grey' },
                { id: 2, text: '60-100', score: 0, selected: true, color: 'grey' },
                { id: 3, text: '101-110', score: 1, selected: false, color: 'grey' },
                { id: 4, text: '111-119', score: 2, selected: false, color: 'grey' },
                { id: 5, text: '>=120', score: 3, selected: false, color: 'grey' },
            ],
            sistRanges: [
                { id: 0, text: '<=70', score: 3, selected: false, color: 'grey' },
                { id: 1, text: '71-89', score: 2, selected: false, color: 'grey' },
                { id: 2, text: '90-139', score: 0, selected: true, color: 'grey' },
                { id: 3, text: '140-159', score: 2, selected: false, color: 'grey' },
                { id: 4, text: '>=160', score: 3, selected: false, color: 'grey' },
            ],
            diastRanges: [
                { id: 0, text: '<=50', score: 3, selected: false, color: 'grey' },
                { id: 1, text: '51-59', score: 2, selected: false, color: 'grey' },
                { id: 2, text: '60-85', score: 0, selected: true, color: 'grey' },
                { id: 3, text: '86-89', score: 1, selected: false, color: 'grey' },
                { id: 4, text: '90-109', score: 2, selected: false, color: 'grey' },
                { id: 5, text: '>=110', score: 3, selected: false, color: 'grey' },
            ],
            frRanges: [
                { id: 0, text: '<=11', score: 3, selected: false, color: 'grey' },
                { id: 1, text: '12-22', score: 0, selected: true, color: 'grey' },
                { id: 2, text: '23-29', score: 2, selected: false, color: 'grey' },
                { id: 3, text: '>=30', score: 3, selected: false, color: 'grey' },
            ],
            scoreColor: 'yellow',
        }
    },
    computed: {
        scoreMAMA() {
            return this.fcRanges.filter(fc => fc.selected == true)[0].score + 
                    this.sistRanges.filter(sist => sist.selected == true)[0].score +
                    this.diastRanges.filter(diast => diast.selected == true)[0].score +
                    this.frRanges.filter(fr => fr.selected == true)[0].score 
        }
    },
    methods: {
        onItemSelected(objArray, id) {
            objArray = objArray.map( arrayElement => {
                if(arrayElement.id == id){
                    arrayElement.selected = true;
                    arrayElement.color = 'green'
                    // this.fcSelected = arrayElement;
                }else{
                    arrayElement.selected = false;
                    arrayElement.color = 'grey'
                }
                return arrayElement
            })
            // this.fcRanges = this.fcRanges.map( fc => {
            //     if(fc.id == id){
            //         fc.selected = true;
            //         fc.color = 'green'
            //         this.fcSelected = fc;
            //     }else{
            //         fc.selected = false;
            //         fc.color = 'grey'
            //     }
            //     return fc
            // })
        }
    },
}
</script>

<style>
    .score-result{
        flex-direction: row;
        justify-content: space-between;
        padding: 20px;
    }
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
