<!-- 
* Collection of components to manipulate styles attributes.
* UI for a style attribute is only generated if:
  a) it is present on the collection of style attributes that was passed on
  from a content element or region.
  b) when it has any effect i.e. it applies to the content element
  from which it is passsed or it is inherited to a descendent content element.
  </style>
  
</style>

</style>

-->
<template>
  <div class="menu">
    <AttrStyle
      v-if="editable('origin$w', regionStyles)"
      :name="'origin$w'"
      :styles="regionStyles"
      :type="'simple'"
      @gotFocus="focusBubble"
    />

    <AttrStyle
      v-if="editable('origin$h', regionStyles)"
      :name="'origin$h'"
      :styles="regionStyles"
      :type="'simple'"
      @gotFocus="focusBubble"
    />

    <AttrStyle
      v-if="editable('extent$w', regionStyles)"
      :name="'extent$w'"
      :styles="regionStyles"
      :type="'simple'"
      @gotFocus="focusBubble"
    />

    <AttrStyle
      v-if="editable('extent$h', regionStyles)"
      :name="'extent$h'"
      :styles="regionStyles"
      :type="'simple'"
      @gotFocus="focusBubble"
    />

    <AttrStyle
      v-if="editable('displayAlign', regionStyles)"
      :name="'displayAlign'"
      :styles="regionStyles"
      :type="'radio'"
      @gotFocus="focusBubble"
    />

    <AttrStyle
      v-if="editable('writingMode', regionStyles)"
      :name="'writingMode'"
      :styles="regionStyles"
      :type="'radio'"
      @gotFocus="focusBubble"
    />

    <AttrStyle
      v-if="editable('showBackground', regionStyles)"
      :name="'showBackground'"
      :styles="regionStyles"
      :type="'radio'"
      @gotFocus="focusBubble"
    />

    <AttrStyle
      v-if="editable('direction')"
      :name="'direction'"
      :styles="styles"
      :type="'radio'"
      @gotFocus="focusBubble"
    />

    <AttrStyle
      v-if="editable('unicodeBidi')"
      :name="'unicodeBidi'"
      :styles="styles"
      :type="'radio'"
      @gotFocus="focusBubble"
    />

    <AttrStyle
      v-if="editable('display')"
      :name="'display'"
      :styles="styles"
      :type="'radio'"
      @gotFocus="focusBubble"
    />

    <AttrStyle
      v-if="editable('textAlign')"
      :name="'textAlign'"
      :styles="styles"
      :type="'radio'"
      @gotFocus="focusBubble"
    />

    <AttrStyle
      v-if="editable('fontWeight')"
      :name="'fontWeight'"
      :styles="styles"
      :type="'radio'"
      @gotFocus="focusBubble"
    />

    <AttrStyle
      v-if="editable('fontStyle')"
      :name="'fontStyle'"
      :styles="styles"
      :type="'radio'"
      @gotFocus="focusBubble"
    />

    <AttrStyle
      v-if="editable('fontSize')"
      :name="'fontSize'"
      :styles="styles"
      :type="'simple'"
      @gotFocus="focusBubble"
    />

    <AttrStyle
      v-if="editable('lineHeight')"
      :name="'lineHeight'"
      :styles="styles"
      :type="'simple'"
      @gotFocus="focusBubble"
    />

    <AttrStyle
      v-if="editable('fillLineGap')"
      :name="'fillLineGap'"
      :styles="styles"
      :type="'radio'"
      @gotFocus="focusBubble"
    />

    <AttrStyle
      v-if="editable('color')"
      :name="'color'"
      :styles="styles"
      :type="'simple'"
      :getter="helper.colorArrayToHexRgb"
      :setter="helper.hexRgbToColorArray"
      @gotFocus="focusBubble"
    />

    <AttrStyle
      v-if="editable('backgroundColor')"
      :name="'backgroundColor'"
      :styles="styles"
      :type="'simple'"
      :getter="helper.colorArrayToHexRgba"
      :setter="helper.hexRgbaToColorArray"
      @gotFocus="focusBubble"
    />

    <AttrStyle
      v-if="editable('fontFamily')"
      :name="'fontFamily'"
      :styles="styles"
      :type="'simple'"
      @gotFocus="focusBubble"
    />

    <AttrStyle
      v-if="editable('multiRowAlign')"
      :name="'multiRowAlign'"
      :styles="styles"
      :type="'radio'"
      @gotFocus="focusBubble"
    />

    <AttrStyle
      v-if="editable('opacity', regionStyles)"
      :name="'opacity'"
      :styles="regionStyles"
      :type="'simple'"
      @gotFocus="focusBubble"
    />
  </div>
</template>

<script>
import { mapState, mapActions } from "vuex";
import AttrStyle from "./AttrStyle.vue";

export default {
  components: {
    AttrStyle
  },
  props: {
    contentKind: {
      type: String,
      required: true
    },
    regionStyles: {
      type: Object,
      required: false
    },
    styles: {
      required: true
    }
  },
  computed: {
    ...mapState(["helper", "styleData"])
  },
  methods: {
    editable(name, styles = this.styles) {
      var isEditable = this.styleData.editable(name, styles, this.contentKind);
      if (this.debug)
        console.log(
          name + " on " + this.contentKind + ": " + isEditable + styles
        );
      return this.styleData.editable(name, styles, this.contentKind);
    },
    focusBubble() {
      this.$emit("gotFocus");
    }
  }
};
</script>

<style scoped>
.menu {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr 1fr 1fr 1fr;
  background-color: #f6f8fa !important;
  color: #24292e !important;
}

.menu div {
  padding: 1vw;
}
</style>