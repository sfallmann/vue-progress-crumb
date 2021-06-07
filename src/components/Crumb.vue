
<template>
  <div class="crumb" :style="crumbStyle">
    <div class="crumb__wrapper" :style="innerWrapperStyle">
      <div v-if="leftIndent" class="crumb__end" :style="innerLeftIndentStyle" />
      <span class="crumb__center" :style="innerCenterStyle">
        <div class="crumb__content" :style="contentStyle">
          <slot>
            <div class="crumb__content__text" :style="textStyle">
              {{ text }}
            </div>
          </slot>
        </div>
      </span>
      <div class="crumb__end" :style="innerRightEndStyle" />
    </div>
    <div
      v-if="borderSize"
      class="crumb__wrapper crumb--outline"
      :style="outerWrapperStyle"
    >
      <div v-if="leftIndent" class="crumb__end" :style="outerLeftIndentStyle" />
      <span class="crumb__center" :style="outerCenterStyle"> </span>
      <div class="crumb__end" :style="outerRightEndStyle" />
    </div>
  </div>
</template>
<script>
export default {
  name: "Crumb",
  props: {
    text: {
      type: String,
      default: "",
    },
    leftIndent: {
      type: Boolean,
      default: false,
    },
    height: {
      type: String,
      default: "60",
    },
    width: {
      type: String,
      default: "auto",
    },
    textColor: {
      type: String,
      default: "white",
    },
    textOpacity: {
      type: String,
      default: "0.85",
    },
    bgColor: {
      type: String,
      default: "gray",
    },
    borderSize: {
      type: Number,
      default: 0,
    },
    borderColor: {
      type: String,
      default: "black",
    },
  },
  computed: {
    widthValue() {
      return Number(this.width);
    },
    heightValue() {
      const height = Number(this.height);
      if (Number.isNaN(height)) return 60;
      return height >= 30 ? height : 30;
    },
    innerCrumbHeight() {
      if (this.borderSize) {
        return this.heightValue - 2 * this.borderSize;
      }
      return this.heightValue;
    },
    outerCrumbWidthDiff() {
      const offset = this.leftIndent ? 2 : 1;
      return (this.heightValue / 3.25) * offset;
    },
    innerCrumbWidth() {
      if (this.borderSize) {
        if (Number.isNaN(this.widthValue)) {
          return `calc(${this.width} - ${this.borderSize}px)`;
        }
        return `${this.width - this.borderSize}px`;
      }
      if (Number.isNaN(this.widthValue)) return this.width;
      return `${this.width}px`;
    },
    outerCrumbWidth() {
      if (Number.isNaN(this.widthValue)) return this.width;
      else return `${this.width}px`;
    },
    outerCrumbCenterWidth() {
      const offset = this.borderSize === 1 ? 1 : 0;

      if (Number.isNaN(this.widthValue))
        return `calc(${this.width} - ${this.outerCrumbWidthDiff}px)`;
      return `${this.widthValue - this.outerCrumbWidthDiff - offset}px`;
    },
    innerCrumbWidthDiff() {
      const offset = this.leftIndent ? 2 : 1;
      return (this.innerCrumbHeight / 3.27) * offset;
    },
    innerCrumbCenterWidth() {
      const multiplier = this.borderSize * 2;
      const offset = this.leftIndent
        ? multiplier + this.borderSize
        : multiplier;

      if (Number.isNaN(this.widthValue)) {
        const vwAdjustment = this.width.includes("vw") ? this.borderSize : 0;

        if (this.borderSize) {
          return `calc(${this.width} + ${this.borderSize}px - ${
            offset + vwAdjustment + this.innerCrumbWidthDiff
          }px)`;
        }

        return `calc(${this.width} - ${this.innerCrumbWidthDiff}px)`;
      }

      if (this.borderSize) {
        return `${this.widthValue - (offset + this.innerCrumbWidthDiff)}px`;
      }

      return `${this.widthValue - this.innerCrumbWidthDiff}px`;
    },
    crumbStyle() {
      return {
        width: this.outerCrumbWidth,
        height: `${this.heightValue}px`,
      };
    },
    innerWrapperStyle() {
      return {
        height: `${this.innerCrumbHeight}px`,
        width: this.innerCrumbWidth,
      };
    },
    innerVertBorderHeight() {
      return this.innerCrumbHeight / 2;
    },
    innerLeftBorderHeight() {
      return this.innerCrumbHeight / 3.27;
    },
    outerVertBorderHeight() {
      return this.heightValue / 2;
    },
    outerLeftBorderHeight() {
      return this.heightValue / 3.27;
    },
    innerLeftIndentStyle() {
      return {
        marginLeft: `${this.borderSize * 2 - this.borderSize / 4}px`,
        borderTop: `${this.innerVertBorderHeight}px solid ${this.bgColor}`,
        borderBottom: `${this.innerVertBorderHeight}px solid ${this.bgColor}`,
        borderLeft: `${this.innerLeftBorderHeight}px solid transparent`,
      };
    },
    innerCenterStyle() {
      return {
        marginLeft: this.leftIndent ? 0 : `${this.borderSize}px`,
        height: `${this.innerCrumbHeight}px`,
        backgroundColor: `${this.bgColor}`,
        width: `${this.innerCrumbCenterWidth}`,
      };
    },
    contentStyle() {
      return {
        maxWidth: `${this.innerCrumbCenterWidth}`,
        maxHeight: `${this.innerCrumbHeight}px`,
      };
    },
    textStyle() {
      return {
        opacity: this.textOpacity,
        color: `${this.textColor}`,
      };
    },
    innerRightEndStyle() {
      return {
        borderTop: `${this.innerVertBorderHeight}px solid transparent`,
        borderBottom: `${this.innerVertBorderHeight}px solid transparent`,
        borderLeft: `${this.innerLeftBorderHeight}px solid ${this.bgColor}`,
      };
    },
    outerWrapperStyle() {
      return {
        top: 0,
        left: 0,
        width: `${this.outerCrumbWidth}`,
      };
    },
    outerLeftIndentStyle() {
      return {
        borderTop: `${this.outerVertBorderHeight}px solid ${this.borderColor}`,
        borderBottom: `${this.outerVertBorderHeight}px solid ${this.borderColor}`,
        borderLeft: `${this.outerLeftBorderHeight}px solid transparent`,
      };
    },
    outerCenterStyle() {
      return {
        height: `${this.heightValue}px`,
        backgroundColor: `${this.borderColor}`,
        width: `${this.outerCrumbCenterWidth}`,
      };
    },
    outerRightEndStyle() {
      return {
        borderTop: `${this.outerVertBorderHeight}px solid transparent`,
        borderBottom: `${this.outerVertBorderHeight}px solid transparent`,
        borderLeft: `${this.outerLeftBorderHeight}px solid ${this.borderColor}`,
      };
    },
  },
};
</script>
<style scoped>
.crumb__center {
  display: inline-block;
  position: relative;
  vertical-align: middle;
}

.crumb__end {
  display: inline-block;
  height: 0;
  vertical-align: middle;
}

.crumb__content {
  padding-left: 10px;
  width: 100%;
  height: 100%;
  display: flex;
  align-items: center;
}
.crumb__content__text {
  width: 100%;
}
.crumb__wrapper {
  position: relative;
  box-sizing: border-box;
}
.crumb {
  box-sizing: border-box;
  position: relative;
  display: flex;
  align-items: center;
  overflow: hidden;
}
.crumb--outline {
  position: absolute;
  z-index: -1;
}
</style>