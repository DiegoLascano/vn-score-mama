<template>
  <nb-container>
    <nb-content class="body-container">
      <nb-view>
        <text class="about-title">Score MAMÁ</text>
        <text class="about-company">NextTech Development</text>
        <text class="about-company"></text>
        <text class="about-subtitle">Versión 1.0.1</text>
        <text class="about-body">
          La presente aplicación móvil está basada en los lineamientos del protocolo “Score MAMÁ
          y claves obstétricas” publicado por el
          <nb-text :style="{ fontWeight: '600' }">Ministerio de Salud Pública&nbsp;</nb-text>en el año 2017, y tiene como objeto
          facilitar el acceso del personal de salud a esta herramienta con apoyo de la tecnología, de una manera
          <nb-text
            :style="{ textDecorationLine: 'underline' }"
          >fácil y sin necesidad de conexión a internet</nb-text>.
        </text>
        <text class="about-body">
          El score MAMÁ permite la estadificación del riesgo obstétrico para facilitar el manejo de las principales
          emergencias obstétricas, mediante la implementación de un sistema de respuesta rápida compuesto por claves:
          <nb-text
            :style="{ backgroundColor: 'rgba(255, 160, 122, 0.5)', color: 'red' }"
          >&nbsp;roja&nbsp;</nb-text>,
          <nb-text
            :style="{ backgroundColor: 'rgba(173, 216, 230, 0.5)', color: 'blue' }"
          >&nbsp;azul&nbsp;</nb-text>,
          <nb-text
            :style="{ backgroundColor: 'rgba(255, 255, 153, 0.8)', color: 'rgb(196, 145, 2)' }"
          >&nbsp;amarilla&nbsp;</nb-text>.
        </text>
        <text class="about-body">
          Su propósito es agilizar y estandarizar lineamientos para la toma de decisiones en
          emergencias obstétricas, que conlleven a los criterios de manejo oportuno de las gestantes y puérperas,
          constituyendo un soporte permanente para el personal de salud que trabaja en la atención de este grupo
          poblacional en los establecimientos de salud de todos los niveles de atención del Sistema Nacional de
          Salud del Ecuador.
        </text>
      </nb-view>
    </nb-content>
  </nb-container>
</template>

<script>
export default {
  props: {
    navigation: {
      type: Object
    }
  }
};
</script>

<style>
.body-container {
  padding: 10px;
}
.about-title {
  font-size: 20px;
  font-weight: bold;
  color: rgb(72, 72, 74);
}
.about-subtitle {
  font-size: 17px;
  font-weight: 500;
  color: rgb(72, 72, 74);
}
.about-company {
  font-size: 14px;
  font-weight: 500;
  color: rgb(72, 72, 74);
}
.about-body {
  margin-top: 20px;
  font-size: 16px;
  color: rgb(72, 72, 74);
}
</style>
