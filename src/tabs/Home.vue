<template>
    <nb-container>
        <view>
            <view 
                :style="{ backgroundColor: 'rgb(242,242,247)', paddingTop: 10 }">
                <touchable-opacity
                    class="score-container"
                    :style="{ backgroundColor: scoreColor, flexDirection: 'row', justifyContent: 'space-between' }"
                    @press="toggleScoreInfo()">
                    <view class="score-up" >
                        <text class="score-sub">Resultado</text> 
                        <!-- <text class="score-sub">Score MAMA</text>  -->
                        <view class="score-down">
                            <nb-text class="score-punctuation">{{ scoreMAMA.score }}</nb-text>
                            <nb-text :style="{ fontSize: 14, color: 'rgb(72, 72, 74)' }">&nbsp;puntos</nb-text>
                        </view>
                    </view>
                    <view class="icon-container">
                        <nb-icon v-if="!showScoreInfo" :style="{ color: 'rgb(44, 44, 46)' }" name='ios-add-circle' /> 
                        <nb-text  v-if="!showScoreInfo" :style="{ fontSize: 12, color: 'rgb(99,99,102)' }">Ver más</nb-text>
                        <nb-icon v-if="showScoreInfo" :style="{ color: 'rgb(44, 44, 46)' }" name='ios-arrow-dropup-circle' /> 
                        <nb-text v-if="showScoreInfo" :style="{ fontSize: 12, color: 'rgb(99,99,102)' }">Ver menos</nb-text>
                    </view>
                </touchable-opacity>
            </view>
            <view
                v-if="showScoreInfo"
                :style="{backgroundColor: 'rgb(242,242,247)', paddingTop: 10 }">
                <view   
                    class="score-container"
                    :style="{ backgroundColor: scoreColor }">
                    <nb-text class="info-title">{{ scoreMAMA.title }}</nb-text>
                        <flat-list
                            :data="scoreMAMA.steps"
                            :render-item="(item) => renderList(item)"
                        />
                </view>
            </view>
        </view>
        <!-- <nb-card>
            <nb-card-item 
                header 
                button 
                bordered
                @press="toggleScoreInfo()" 
                :style="{ backgroundColor: scoreColor, padding: 20, flexDirection: 'row', justifyContent: 'space-between', borderRadius: 20 }">
                <view class="score-up" >
                    <text class="score-sub">Score MAMA</text> 
                    <view class="score-down">
                        <nb-text class="score-punctuation">{{ scoreMAMA.score }}</nb-text>
                        <nb-text :style="{ fontSize: 14, color: '#29293d' }">&nbsp;puntos</nb-text>
                    </view>
                </view>
                <view class="icon-container">
                    <nb-icon v-if="!showScoreInfo" :style="{ color: '#5c5c8a' }" name='ios-add-circle' /> 
                    <nb-text  v-if="!showScoreInfo" :style="{ fontSize: 12, color: '#29293d' }">Ver más</nb-text>
                    <nb-icon v-if="showScoreInfo" :style="{ color: '#5c5c8a' }" name='ios-arrow-dropup-circle' /> 
                    <nb-text v-if="showScoreInfo" :style="{ fontSize: 12, color: '#29293d' }">Ver menos</nb-text>
                </view>
            </nb-card-item>
            <nb-card-item 
                v-if="showScoreInfo"
                bordered
                :style="{ backgroundColor: scoreColor }">
                    <nb-body>
                        <nb-text class="info-title">{{ scoreMAMA.title }}</nb-text>
                            <flat-list
                                :data="scoreMAMA.steps"
                                :render-item="(item) => renderList(item)"
                            />
                    </nb-body>
            </nb-card-item>
        </nb-card> -->
        <nb-content class="body-container">
            <text class="options-label">Tipo de establecimiento</text>
            <view class="options-container">
                <Picker :array="establecimientos" />
            </view>
            <text class="options-label">Frecuencia Cardíaca</text>
            <view class="options-container">
                <Selectable :array="frecuenciaCardiaca"></Selectable>
            </view>
            <text class="options-label">Presión Sistólica</text>
            <view class="options-container">
                <Selectable :array="sistolica"></Selectable>
            </view>
            <text class="options-label">Presión Diastólica</text>
            <view class="options-container">
                <Selectable :array="diastolica"></Selectable>
            </view>
            <text class="options-label">Frecuencia Respiratoria</text>
            <view class="options-container">
                <Selectable :array="frecuenciaRespitatoria"></Selectable>
            </view>
            <text class="options-label">Temperatura</text>
            <view class="options-container">
                <Selectable :array="temperatura"></Selectable>
            </view>
            <text class="options-label">Saturación</text>
            <view class="options-container">
                <Selectable :array="saturacion"></Selectable>
            </view>
            <text class="options-label">Estado de Conciencia</text>
            <view class="options-container">
                <Picker :array="conciencia" />
            </view>
            <text class="options-label">Proteinuria</text>
            <view class="options-container options-end">
                <Picker :array="proteinuria" />
            </view>
        </nb-content>
    </nb-container>
</template>

<script>
import React from 'react'
import { Text, View } from 'native-base'
import Selectable from '../components/Selectable';
import Picker from '../components/Picker';
export default {
    components: {
        Selectable,
        Picker,
    },
    props: {
        navigation: {
            type: Object
        },
    },
    data() {
        return {
            frecuenciaCardiaca: [
                { id: 0, text: '<=50', score: 3, selected: false, color: 'grey' },
                { id: 1, text: '51-59', score: 1, selected: false, color: 'grey' },
                { id: 2, text: '60-100', score: 0, selected: true, color: 'grey' },
                { id: 3, text: '101-110', score: 1, selected: false, color: 'grey' },
                { id: 4, text: '111-119', score: 2, selected: false, color: 'grey' },
                { id: 5, text: '>=120', score: 3, selected: false, color: 'grey' },
            ],
            sistolica: [
                { id: 0, text: '<=70', score: 3, selected: false, color: 'grey' },
                { id: 1, text: '71-89', score: 2, selected: false, color: 'grey' },
                { id: 2, text: '90-139', score: 0, selected: true, color: 'grey' },
                { id: 3, text: '140-159', score: 2, selected: false, color: 'grey' },
                { id: 4, text: '>=160', score: 3, selected: false, color: 'grey' },
            ],
            diastolica: [
                { id: 0, text: '<=50', score: 3, selected: false, color: 'grey' },
                { id: 1, text: '51-59', score: 2, selected: false, color: 'grey' },
                { id: 2, text: '60-85', score: 0, selected: true, color: 'grey' },
                { id: 3, text: '86-89', score: 1, selected: false, color: 'grey' },
                { id: 4, text: '90-109', score: 2, selected: false, color: 'grey' },
                { id: 5, text: '>=110', score: 3, selected: false, color: 'grey' },
            ],
            frecuenciaRespitatoria: [
                { id: 0, text: '<=11', score: 3, selected: false, color: 'grey' },
                { id: 1, text: '12-22', score: 0, selected: true, color: 'grey' },
                { id: 2, text: '23-29', score: 2, selected: false, color: 'grey' },
                { id: 3, text: '>=30', score: 3, selected: false, color: 'grey' },
            ],
            temperatura: [
                { id: 0, text: '<=35.5', score: 2, selected: false, color: 'grey' },
                { id: 1, text: '35.6-37.5', score: 0, selected: true, color: 'grey' },
                { id: 2, text: '37.6-38.4', score: 1, selected: false, color: 'grey' },
                { id: 3, text: '>=38.5', score: 3, selected: false, color: 'grey' },
            ],
            saturacion: [
                { id: 0, text: '<=85', score: 3, selected: false, color: 'grey' },
                { id: 1, text: '86-89', score: 2, selected: true, color: 'grey' },
                { id: 2, text: '90-93', score: 1, selected: false, color: 'grey' },
                { id: 3, text: '94-100', score: 0, selected: false, color: 'grey' },
            ],
            conciencia: [
                { label: 'Confusa/agitada', value: 'key0', score: 2, selected: false },
                { label: 'Alerta', value: 'key1', score: 0, selected: true },
                { label: 'Responde a la voz/somnolienta', value: 'key2', score: 1, selected: false },
                { label: 'Responde al dolor/estuporosa', value: 'key3', score: 2, selected: false },
                { label: 'No responde', value: 'key4', score: 3, selected: false },
            ],
            proteinuria: [
                { label: 'Negativo', value: 'key0', score: 0, selected: true },
                { label: 'Positivo', value: 'key1', score: 1, selected: true },
            ],
            scoreSteps:[
                {
                    establecimiento: 'AB',
                    data: [
                        {score: 0, title: 'Evaluar y analizar factores de riesgo, bienestar materno-fetal y signos de alarma', steps: ''},
                        {score: 1, title: 'Evaluar y analizar factores de riesgo', steps: [
                            {key: '0', step: '1. Aplique el Score MAMA c/4 horas y registre.'},
                            {key: '1', step: '2. Reevalúe signos vitales y signos de alarma materna.'},
                            {key: '2', step: '3. Evalúe factores de riesgo'},
                            {key: '3', step: '4. Realice pruebas de bienestar fetal básicas utilizando estetoscopio, Doppler fetal o campana de Pinar.'},
                            {key: '4', step: '5. Considere exámenes complementarios y/o evaluación por interconsulta con especialiasta.'},
                            {key: '5', step: '6. Si se revierte el puntaje, envíe a la casa y realice seguimiento (Agendar cita).'},
                        ]},
                        {score: 2, title: 'Trate y refiera según el caso ', steps: [
                            {key: '0', step: '1. Aplique el Score MAMA c/hora y registre.'},
                            {key: '1', step: '2. Reevalúe signos vitales y signos de alarma.'},
                            {key: '2', step: '3. Realice un diagnóstico primario basado en el cuadro clínico.'},
                            {key: '3', step: '4. Realice pruebas de bienestar fetal básicas utilizando estetoscopio, Doppler fetal o campana de Pinar'},
                            {key: '4', step: '5. Aliste, active y aplique CLAVE AZUL, ROJA o AMARILLA, según sea el caso.'},
                            {key: '5', step: '6. Elabore la referencia (053) y envíe a nivel de mayor capacidad resolutiva según el caso.'},
                            {key: '6', step: '7. Transfiera (acompañada por un profesional de salud).'},
                            {key: '7', step: '8. Active cadena de llamadas: comunique al Director del establecimiento de salud y éste al DirectorDistrital.'},
                            {key: '8', step: '9. Realice el seguimiento del caso.'},
                        ]},
                        {score: 3, title: 'Trate y refiera según el caso', steps: [
                            {key: '0', step: '1. Aplique el Score MAMA c/hora y registre.'},
                            {key: '1', step: '2. Reevalúe signos vitales y signos de alarma.'},
                            {key: '2', step: '3. Realice un diagnóstico primario basado en el cuadro clínico.'},
                            {key: '3', step: '4. Realice pruebas de bienestar fetal básicas utilizando estetoscopio, Doppler fetal o campana de Pinar'},
                            {key: '4', step: '5. Aliste, active y aplique CLAVE AZUL, ROJA o AMARILLA, según sea el caso.'},
                            {key: '5', step: '6. Elabore la referencia (053) y envíe a nivel de mayor capacidad resolutiva según el caso.'},
                            {key: '6', step: '7. Transfiera (acompañada por un profesional de salud).'},
                            {key: '7', step: '8. Active cadena de llamadas: comunique al Director del establecimiento de salud y éste al DirectorDistrital.'},
                            {key: '8', step: '9. Realice el seguimiento del caso.'},
                        ]},
                        {score: 4, title: 'Trate y refiera según el caso', steps: [
                            {key: '0', step: '1. Aplique el Score MAMA c/hora y registre.'},
                            {key: '1', step: '2. Reevalúe signos vitales y signos de alarma.'},
                            {key: '2', step: '3. Realice un diagnóstico primario basado en el cuadro clínico.'},
                            {key: '3', step: '4. Realice pruebas de bienestar fetal básicas utilizando estetoscopio, Doppler fetal o campana de Pinar'},
                            {key: '4', step: '5. Aliste, active y aplique CLAVE AZUL, ROJA o AMARILLA, según sea el caso.'},
                            {key: '5', step: '6. Elabore la referencia (053) y envíe a nivel de mayor capacidad resolutiva según el caso.'},
                            {key: '6', step: '7. Transfiera (acompañada por un profesional de salud).'},
                            {key: '7', step: '8. Active cadena de llamadas: comunique al Director del establecimiento de salud y éste al Director Distrital.'},
                            {key: '8', step: '9. Realice el seguimiento del caso.'},
                        ]},
                        {score: 5, title: 'Trate y refiera según el caso', steps: [
                            {key: '0', step: '1. Aplique el Score MAMA c/30 minutos y registre.'},
                            {key: '1', step: '2. Reevalúe signos vitales y signos de alarma.'},
                            {key: '2', step: '3. Realice pruebas de bienestar fetal básicas utilizando estetoscopio, Doppler fetal o campana dePinar'},
                            {key: '3', step: '4. Aliste, active y aplique CLAVE AZUL, ROJA o AMARILLA, según sea el caso.'},
                            {key: '4', step: '5. Elabore la referencia (053) y envíe aestablecimiento de salud de mayor complejidad según la emergencia obstétrica.'},
                            {key: '5', step: '6. Transfiera (acompañada por un profesional de salud).'},
                            {key: '6', step: '7. Active cadena de llamadas: comunique al Director del establecimiento de salud y éste al Director Distrital o Coordinador Zonal.'},
                            {key: '7', step: '8. Realice el seguimiento del caso.'},
                        ]},
                    ],
                },
                {
                    establecimiento: 'C',
                    data: [
                        {score: 0, title: 'Evaluar y analizar factores de riesgo, bienestar materno-fetal y signos de alarma', steps: ''},
                        {score: 1, title: 'Evaluar y analizar factores de riesgo', steps: [
                            {key: '0', step: '1. Aplique el Score MAMA c/4 horas y registre.'},
                            {key: '1', step: '2. Reevalúe signos vitales.'},
                            {key: '2', step: '3. Evalúe factores de riesgo y signos de alarma materna'},
                            {key: '3', step: '4. Realice pruebas de bienestar fetal básicas utilizando estetoscopio, Doppler fetal o campana de Pinar.'},
                            {key: '4', step: '5. Considere exámenes complementarios y/o evaluación por interconsulta con especialiasta.'},
                            {key: '5', step: '6. Si se revierte el puntaje, envíe a la casa y realice seguimiento (Agendar cita).'},
                        ]},
                        {score: 2, title: 'Trate y refiera según el caso ', steps: [
                            {key: '0', step: '1. Aplique el Score MAMA c/hora y registre.'},
                            {key: '1', step: '2. Evalúe signos vitales más signos de alarma.'},
                            {key: '2', step: '3. Realice un diagnóstico primario basado en el cuadro clínico.'},
                            {key: '3', step: '4. Comunique al médico tratante quien debe evaluar en máximo 30 minutos.'},
                            {key: '4', step: '5. Aliste, active y aplique CLAVE AZUL, ROJA o AMARILLA, según sea el caso.'},
                            {key: '5', step: '6. Si no revierte el puntaje en una hora, evalúe signos de alarma materna y bienestar fetal; y realice referencia a establecimiento de mayor complejidad, dependiendo del tipo de complicación obstétrica.'},
                            {key: '6', step: '7. Transfiera (acompañada por un profesional de salud).'},
                            {key: '7', step: '8. Active cadena de llamadas: comunique al Director del establecimiento de salud y éste al Director Distrital o Coordinador Zonal.'},
                            {key: '8', step: '9. Si revierte puntaje use los pasos correspondientes.'},
                        ]},
                        {score: 3, title: 'Trate y refiera según el caso', steps: [
                            {key: '0', step: '1. Aplique el Score MAMA c/hora y registre.'},
                            {key: '1', step: '2. Evalúe signos vitales más signos de alarma.'},
                            {key: '2', step: '3. Realice un diagnóstico primario basado en el cuadro clínico.'},
                            {key: '3', step: '4. Comunique al médico tratante quien debe evaluar en máximo 30 minutos.'},
                            {key: '4', step: '5. Aliste, active y aplique CLAVE AZUL, ROJA o AMARILLA, según sea el caso.'},
                            {key: '5', step: '6. Si no revierte el puntaje en una hora, evalúe signos de alarma materna y bienestar fetal; y realice referencia a establecimiento de mayor complejidad, dependiendo del tipo de complicación obstétrica.'},
                            {key: '6', step: '7. Transfiera (acompañada por un profesional de salud).'},
                            {key: '7', step: '8. Active cadena de llamadas: comunique al Director del establecimiento de salud y éste al Director Distrital o Coordinador Zonal.'},
                            {key: '8', step: '9. Si revierte puntaje use los pasos correspondientes.'},
                        ]},
                        {score: 4, title: 'Trate y refiera según el caso', steps: [
                            {key: '0', step: '1. Aplique el Score MAMA c/hora y registre.'},
                            {key: '1', step: '2. Evalúe signos vitales más signos de alarma.'},
                            {key: '2', step: '3. Realice un diagnóstico primario basado en el cuadro clínico.'},
                            {key: '3', step: '4. Comunique al médico tratante quien debe evaluar en máximo 30 minutos.'},
                            {key: '4', step: '5. Aliste, active y aplique CLAVE AZUL, ROJA o AMARILLA, según sea el caso.'},
                            {key: '5', step: '6. Si no revierte el puntaje en una hora, evalúe signos de alarma materna y bienestar fetal; y realice referencia a establecimiento de mayor complejidad, dependiendo del tipo de complicación obstétrica.'},
                            {key: '6', step: '7. Transfiera (acompañada por un profesional de salud).'},
                            {key: '7', step: '8. Active cadena de llamadas: comunique al Director del establecimiento de salud y éste al Director Distrital o Coordinador Zonal.'},
                            {key: '8', step: '9. Si revierte puntaje use los pasos correspondientes.'},
                        ]},
                        {score: 5, title: 'Trate y refiera según el caso', steps: [
                            {key: '0', step: '1. Aplique el Score MAMA c/30 minutos y registre.'},
                            {key: '1', step: '2. Evalúe signos vitales más signos de alarma.'},
                            {key: '2', step: '3. Realice un diagnóstico primario basado en el cuadro clínico.'},
                            {key: '3', step: '4. Comunique al médico tratante quien debe evaluar a la paciente en máximo 15 minutos.'},
                            {key: '4', step: '5. Aliste, active y aplique CLAVE AZUL, ROJA o AMARILLA, según sea el caso.'},
                            {key: '5', step: '6. Si no revierte el puntaje en una hora, evalúe signos de alarma materna y bienestar fetal; y realice referencia a establecimiento de mayor complejidad, dependiendo del tipo de complicación obstétrica.'},
                            {key: '6', step: '7. Transfiera acompañamiento de un profesional de salud a nivel superior según el caso.'},
                            {key: '7', step: '8. Active cadena de llamadas: comunique al Director del establecimiento de salud y éste al Director Distrital o Coordinador Zonal.'},
                            {key: '8', step: '9. Si revierte puntaje use los pasos correspondientes.'},
                        ]},
                    ],
                }
            ],
            establecimientos: [
                { type:'AB', label: 'Puesto de salud, Centros de salud tipo A, B, y de atención prehospitalaria', value: 'key0', selected: true },
                { type:'C', label: 'Establecimientos Tipo C y hospitales básicos', value: 'key1', selected: false },
            ],
            scoreColor: '',
            showScoreInfo: false,
            scoreMAMAReal: 0,
        }
    },
    computed: {
        scoreMAMA() {
            value =  this.frecuenciaCardiaca.filter( fc => fc.selected == true )[0].score + 
                this.sistolica.filter( sist => sist.selected == true )[0].score +
                this.diastolica.filter( diast => diast.selected == true )[0].score +
                this.frecuenciaRespitatoria.filter( fr => fr.selected == true )[0].score +
                this.temperatura.filter( fr => fr.selected == true )[0].score +
                this.saturacion.filter( fr => fr.selected == true )[0].score +
                this.conciencia.filter( state => state.selected == true )[0].score +
                this.proteinuria.filter( proteinuria => proteinuria.selected == true )[0].score;

            this.scoreMAMAReal = value;

            if(value == 0) this.scoreColor = '#00cc99';
            else if(value == 1) this.scoreColor = '#fff2e6';
            else if(value >= 2 && value <= 4) this.scoreColor = '#ffcc99';
            else if(value >= 5) this.scoreColor = '#ff7733';

            var tipoHospital = this.establecimientos.filter( establecimiento => establecimiento.selected == true )[0]

            var scoreInfoSteps= [];
            if(tipoHospital.type == 'AB') scoreInfoSteps = this.scoreSteps.filter(element => element.establecimiento == 'AB');
            else if(tipoHospital.type == 'C') scoreInfoSteps = this.scoreSteps.filter(element => element.establecimiento == 'C');

            return scoreInfoSteps[0].data.filter(step => {
                if(step.score == value) {
                    return true;
                }else if((value >= 5) && (step.score == 5 )){
                    return true;
                }
            })[0];
        }
    },
    methods: {
        toggleScoreInfo() {
            this.showScoreInfo = ! this.showScoreInfo
        },
        renderList(item) {
            return (<Text style={{ paddingTop: 7, color: 'rgb(72, 72, 74)' }}>{item.item.step}</Text>)
        }
    },
}
</script>

<style>
    .body-container{
        padding-top: 10px;
        background-color: rgb(242,242,247);/* color from iOS light theme */
    }
    .score-container{
        padding: 10; 
        border-radius: 10; 
        margin-left: 10;
        margin-right: 10;
    }
    .score-up{
        /* position: relative; */
        /* width: 100%; */
        flex-direction: column;
        justify-content: space-between;
    }
    .score-down{
        /* width: 100%; */
        flex-direction: row;
        justify-content: flex-start;
        align-items: baseline;
    }
    .score-punctuation{
        color: #5c5c8a;
        font-size: 48px;
        font-weight: 800;
        color: rgb(44, 44, 46);
    }
    .score-sub{
        padding-bottom: 15px;
        font-size: 14px;
        font-weight: 400;
        color: rgb(72, 72, 74);
    }
    .icon-container{
        flex-direction: column;
        align-items: flex-end;
    }
    .info-title{
        font-weight: 600;
        text-align: center;
        padding: 5px;
    }
    /* .info-item{
        font-weight: 300;
        padding: 5px;
    } */
    .options-container{
        margin: 10px;
        background-color: white;
        padding-left: 10px;
        padding-right: 10px;
        padding-top: 20px;
        padding-bottom: 20px;
        border-radius: 10px;
    }
    .options-label{
        /* padding: 10px; */
        margin-top: 15px;
        margin-left: 10px;
        margin-right: 10px;
        color: rgb(72, 72, 74);
        /* background-color: white; */
    }
    .options-end{
        margin-bottom: 20px;
    }
</style>
