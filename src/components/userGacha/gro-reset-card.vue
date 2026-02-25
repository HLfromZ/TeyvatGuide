<!-- 垫数卡片 -->
<template>
  <div class="gro-rc-box">
    <div class="gro-rc-progress" />
    <span>距上个{{ props.compute }}星</span>
    <span>{{ props.count }}</span>
  </div>
</template>
<script lang="ts" setup>
import { computed } from "vue";

type GroResetCardProps = {
  /** 计算星级 */
  compute: "4" | "5";
  /** 祈愿类型 */
  gacha: string;
  /** 当前垫数 */
  count: number;
};

const props = defineProps<GroResetCardProps>();
const color = computed<string>(() => {
  if (props.compute === "4") return "#c678dd";
  return "#d19a66";
});
const width = computed<string>(() => {
  let final = 10;
  if (props.compute === "5") {
    if (props.gacha === "302") final = 80;
    else final = 90;
  }
  return ((props.count / final) * 100).toFixed(2) + "%";
});
</script>
<style lang="scss" scoped>
.gro-rc-box {
  position: relative;
  display: flex;
  overflow: hidden;
  height: 28px;
  align-items: center;
  justify-content: center;
  padding: 8px 4px;
  border: 1px solid v-bind(color);
  border-radius: 4px;
  color: v-bind(color);
  column-gap: 8px;
  font-size: 14px;

  span {
    z-index: 1;
  }
}

.gro-rc-progress {
  position: absolute;
  z-index: 0;
  top: 0;
  left: 0;
  width: v-bind(width);
  height: 100%;
  background: v-bind(color);
  opacity: 0.3;
}
</style>
