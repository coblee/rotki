<template>
  <div
    class="defi-protocol-icon d-flex flex-row align-center"
    :class="mode === 'icon' ? 'justify-center' : null"
  >
    <v-tooltip top :disabled="mode !== 'icon'" open-delay="300ms">
      <template #activator="{ on, attrs }">
        <v-img
          v-if="mode === 'icon' || mode === 'both'"
          contain
          v-bind="attrs"
          max-width="24px"
          max-height="24"
          class="defi-protocol-icon__image mr-2"
          :src="require(`@/assets/images/defi/${protocol}.svg`)"
          v-on="on"
        />
        <span
          v-if="mode === 'label' || mode === 'both'"
          class="defi-protocol-icon__label text--secondary"
        >
          {{ name | capitalize }}
        </span>
      </template>
      <span>
        {{ name | capitalize }}
      </span>
    </v-tooltip>
  </div>
</template>
<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator';
import { DEFI_MAKERDAO, DEFI_YEARN_VAULTS } from '@/services/defi/consts';
import { SupportedDefiProtocols } from '@/services/defi/types';

@Component({})
export default class DefiProtocolIcon extends Vue {
  @Prop({ required: true, type: String })
  protocol!: SupportedDefiProtocols;
  @Prop({ required: false, type: String, default: 'both' })
  mode!: 'icon' | 'label' | 'both';

  get name(): string {
    if (this.protocol === DEFI_MAKERDAO) {
      return 'MakerDAO DSR';
    } else if (this.protocol === DEFI_YEARN_VAULTS) {
      return 'yearn.finance Vaults';
    }
    return this.protocol;
  }
}
</script>

<style lang="scss" scoped>
.defi-protocol-icon {
  &--icon {
    max-width: 30px;
  }

  &__label {
    font-size: 12px;
  }
}
</style>
