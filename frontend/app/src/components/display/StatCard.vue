<template>
  <v-card class="stat-card d-flex flex-columns pa-0 fill-height">
    <div v-if="bordered" class="stat-card__border">
      <div class="stat-card__image ma-2">
        <v-img
          v-if="protocolIcon"
          contain
          alt="Protocol Logo"
          height="36px"
          width="36px"
          :src="protocolIcon"
        />
      </div>
      <div class="stat-card__border__gradient" />
    </div>
    <div class="stat-card__content flex-grow-1">
      <v-card-title class="py-2">
        <span v-if="title">
          {{ title }}
        </span>
        <v-spacer v-if="locked" />
        <premium-lock v-if="locked" />
      </v-card-title>
      <v-card-text>
        <span v-if="!locked && loading">
          <v-progress-linear indeterminate color="primary" />
        </span>
        <slot v-else-if="!locked" />
      </v-card-text>
    </div>
  </v-card>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator';
import PremiumLock from '@/components/helper/PremiumLock.vue';

@Component({
  components: { PremiumLock }
})
export default class StatCard extends Vue {
  @Prop({ required: false })
  title!: string;
  @Prop({ required: false, type: Boolean, default: false })
  locked!: boolean;
  @Prop({ required: false, type: Boolean, default: false })
  loading!: boolean;
  @Prop({ required: false, type: String })
  protocolIcon!: string;
  @Prop({ required: false, type: Boolean, default: false })
  bordered!: boolean;
}
</script>

<style scoped lang="scss">
.stat-card {
  width: 100%;
  min-height: 130px;

  ::v-deep {
    .v-card {
      &__text {
        padding-top: 12px;
        font-size: 1em;
      }
    }
  }

  &__border {
    width: 48px;
    border-radius: 4px 0 0 4px !important;
    background-color: var(--v-rotki-light-grey-darken1);

    &__gradient {
      display: block;
      position: absolute;
      top: 0;
      left: 0;
      height: 100%;
      width: 48px;
      background: linear-gradient(115deg, rgba(255, 0, 0, 0), white);
    }
  }
}
</style>
