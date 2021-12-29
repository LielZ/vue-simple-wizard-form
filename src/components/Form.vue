<template>
    <div class="steps">
        <span :class="{ 'active' : step >= 1}"></span>
        <span :class="{ 'active' : step >= 2}"></span>
        <span :class="{ 'active' : step >= 3}"></span>
    </div>
    <div class="title">
        <h1>שאלה {{step}}</h1>
    </div>
    <div class="desc">
        <p v-if="step === 1">
            היי בואו נתחיל עם שם
        </p>
        <p v-if="step === 2">
            היי {{stepOne.name}},
            על מנת שנוכל לעזור לך לשים את כספך באפיק הנכון, נא לסמן את המקומות בהם יש לך כסף:
        </p>
        <p v-if="step === 3">
            כמעט סיימנו
        </p>
    </div>
    <Step1
        v-if="step === 1"
        v-model:name="stepOne.name"
    />
    <Step2
        v-else-if="step === 2"
        v-model:values="stepTwo.values"
    />
    <Step3  v-else
            :name="stepOne.name"
            :values="stepTwo.values" />
    <div class="justify-content-evenly">
        <button class="btn btn-primary float-end" v-if="step > 1" @click="step -= 1; this.stepTwo.values = [];">אחורה</button>
        <button class="btn btn-primary float-start"  v-if="step < 3" @click="step += 1" :disabled="!this.nextButton">לשלב הבא</button>
        <button class="btn btn-primary float-start" v-else @click="submit">שלח</button>
    </div>
</template>

<script>
    import Step1 from './steps/step1.vue'
    import Step2 from './steps/step2.vue'
    import Step3 from './steps/step3.vue'

    export default {
        name: "Form",
        components: {
            Step1,
            Step2,
            Step3
        },
        data() {
            return {
                step: 1,
              stepOne: {
                  name: '',
              },
              stepTwo: {
                values: [],
              }
            }
        },
      computed: {
        nextButton() {
          if (this.step == 1) {
            return this.stepOne.name.length > 0;
          } else
          {
            return this.stepTwo.values.length > 0;
          }
        }
      }

    }




</script>

<style scoped>
    .steps span.active {
        border: 3px solid #7878dc;
        width: auto;
        min-width: 15%;
        display: inline-block;
        margin-right: 5px;
        border-radius: 5px;
    }

    .steps span {
        border: 3px solid #9b9b9b;
        width: auto;
        min-width: 15%;
        display: inline-block;
        margin-right: 5px;
        border-radius: 5px;
    }

    .title h1 {
        text-align: right;
        color: #bebebe;
        font-weight: 400;
        font-size: 2.50rem;
    }

    .desc p {
        color: #363c8a;
        text-align: right;
        font-size: 1.4rem;
    }
    button {
      background: #363c8a;
      padding: 15px;
      border-radius: 20px;
    }

</style>
