<template>
  <demo-block card>
    <van-cell center :title="t('basicUsage')">
      <template #value>
        <van-stepper v-model="stepper1" />
      </template>
    </van-cell>

    <van-cell center :title="t('step')">
      <template #value>
        <van-stepper v-model="stepper2" step="2" />
      </template>
    </van-cell>

    <van-cell center :title="t('range')">
      <template #value>
        <van-stepper v-model="stepper3" :min="5" :max="8" />
      </template>
    </van-cell>

    <van-cell center :title="t('integer')">
      <template #value>
        <van-stepper v-model="stepper4" integer />
      </template>
    </van-cell>

    <van-cell center :title="t('disabled')">
      <template #value>
        <van-stepper v-model="stepper5" disabled />
      </template>
    </van-cell>

    <van-cell center :title="t('disableInput')">
      <template #value>
        <van-stepper v-model="disabledInput" disable-input />
      </template>
    </van-cell>

    <van-cell center :title="t('decimalLength')">
      <template #value>
        <van-stepper v-model="stepper8" :decimal-length="1" step="0.2" />
      </template>
    </van-cell>

    <van-cell center :title="t('customSize')">
      <template #value>
        <van-stepper v-model="stepper7" button-size="32px" input-width="40px" />
      </template>
    </van-cell>

    <van-cell center :title="t('beforeChange')">
      <template #value>
        <van-stepper v-model="stepper6" :before-change="beforeChange" />
      </template>
    </van-cell>

    <van-cell v-if="!isWeapp" center :title="t('roundTheme')">
      <template #value>
        <van-stepper
          v-model="stepperRound"
          theme="round"
          button-size="22"
          disable-input
        />
      </template>
    </van-cell>
  </demo-block>
</template>

<script lang="ts">
import { reactive, toRefs } from 'vue';
import { useTranslate } from '@demo/use-translate';
import { Toast } from '../../toast';

const i18n = {
  'zh-CN': {
    step: '步长设置',
    range: '限制输入范围',
    integer: '限制输入整数',
    roundTheme: '圆角风格',
    customSize: '自定义大小',
    beforeChange: '异步变更',
    disableInput: '禁用输入框',
    decimalLength: '固定小数位数',
  },
  'en-US': {
    step: 'Step',
    range: 'Range',
    integer: 'Integer',
    roundTheme: 'Round Theme',
    customSize: 'Custom Size',
    beforeChange: 'Before Change',
    disableInput: 'Disable Input',
    decimalLength: 'Decimal Length',
  },
};

export default {
  setup() {
    const t = useTranslate(i18n);
    const state = reactive({
      stepper1: 1,
      stepper2: 1,
      stepper3: 1,
      stepper4: 1,
      stepper5: 1,
      stepper6: 1,
      stepper7: 1,
      stepper8: 1,
      stepperRound: 1,
      disabledInput: 1,
    });

    const beforeChange = () => {
      Toast.loading({ forbidClick: true });

      return new Promise((resolve) => {
        setTimeout(() => {
          Toast.clear();
          resolve(true);
        }, 500);
      });
    };

    return {
      ...toRefs(state),
      t,
      beforeChange,
    };
  },
};
</script>
