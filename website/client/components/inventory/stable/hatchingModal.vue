<template lang="pug">
b-modal#hatching-modal(@change="resetHatchablePet($event)")
  div.content(v-if="hatchablePet")
    div.potionEggGroup
      div.potionEggBackground
        div(:class="'Pet_HatchingPotion_'+hatchablePet.potionKey")
      div.potionEggBackground
        div(:class="'Pet_Egg_'+hatchablePet.eggKey")
    h4.title {{ hatchablePet.name }}
    div.text(v-html="$t('hatchDialogText', { potionName: hatchablePet.potionName, eggName: hatchablePet.eggName, petName: hatchablePet.name })")
  span.svg-icon.icon-10(v-html="icons.close", slot="modal-header", @click="closeHatchPetDialog()")
  div(slot="modal-footer")
    button.btn.btn-primary(@click="hatchPet(hatchablePet)") {{ $t('hatch') }}
    button.btn.btn-secondary.btn-flat(@click="closeHatchPetDialog()") {{ $t('cancel') }}
</template>

<style lang="scss">
  @import '~client/assets/scss/modal.scss';

  #hatching-modal {
    @include centeredModal();

    .modal-dialog {
      width: 310px;
    }

    .content {
      text-align: center;
      margin: 9px;
    }

    .title {
      margin-top: 24px;
      font-size: 20px;
      font-weight: bold;
      line-height: 1.2;
      text-align: center;
      color: #4e4a57;
    }

    .text {
      height: 60px;
      font-size: 14px;
      line-height: 1.43;
      text-align: center;
      color: #686274;
    }

    span.svg-icon.icon-10 {
      position: absolute;
      right: 10px;
      top: 10px;
    }

    .modal-footer {
      justify-content: center;
    }
  }
</style>

<script>
import svgClose from 'assets/svg/close.svg';

import petMixin from 'client/mixins/petMixin';

export default {
  props: ['hatchablePet'],
  mixins: [petMixin],
  data () {
    return {
      icons: Object.freeze({
        close: svgClose,
      }),
    };
  },
  methods: {
    resetHatchablePet ($event) {
      if (!$event) {
        this.hatchablePet = null;
      }
    },
  },
};
</script>
