<template>
  <ion-page>
    <ion-header :translucent="true">
      <ion-toolbar>
        <ion-title>Blank</ion-title>
        <ion-back-button slot="end"></ion-back-button>
      </ion-toolbar>
    </ion-header>
    <ion-content class="ion-padding">
      <ion-button @click="scan">Scanner un code barre</ion-button>
      <pre>
        initial values {{ form }}
        errors  {{ errors }}
        form values {{ values }}
        vinData {{ vinData }}
      </pre>
    </ion-content>
  </ion-page>
</template>

<script>
import {
  defineComponent
} from 'vue'
import {
  IonHeader,
  IonTitle,
  IonButton,
  IonToolbar,
  IonPage,
//  IonInput,
  IonContent,
  IonBackButton
} from '@ionic/vue'
import { BarcodeScanner } from '@ionic-native/barcode-scanner'
import { sample } from 'lodash'
export default defineComponent({
  name: 'Scan',
  components: {
    IonHeader,
    IonTitle,
    IonButton,
    IonToolbar,
  //  IonInput,
    IonPage,
    IonBackButton,
    IonContent,
  },
  data () {
    return {
      vin: null,
      vinData: {},
      form: {
        vin: ''
      },
      schema: {
        vin: 'required'
      }
    }
  },
  methods: {
    async populateVin () {
      const vins = [
        '4Y1SL65848Z411439',
        '1GNALDEK9FZ108495',
        '2C4RDGBG6ER405565',
        'WDBNG75J04A417726',
        '1FAHP3F20CL266328',
        '5XYZWDLA4EG145416',
        'JTDKB20U497855273',
      ]
      this.form.vin = sample(vins)
      console.info(this.form.vin)

    },
    async onSubmit (values) {
      console.log(values)
    },
    async scan () {
      try {
        const data = await BarcodeScanner.scan()
        console.info(`Barcode data: ${data.text}`)
        this.vinData = data
        this.form.vin = data.text
      } catch (e) {
        console.info(e)
      }
    }
  }
})
</script>
