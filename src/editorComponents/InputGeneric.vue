<!-- Simple UI component for text values -->
<template>
  <div :class="[className]">
    <label>
      {{ labelName }}
      <input
        type="text"
        :value="value"
        @change="changedValue"
        @focus="focusBubble"
      />
    </label>
  </div>
</template>

<script>
export default {
  props: {
    value: {
      required: true
    },
    labelName: {
      type: String || Number,
      required: true
    }
  },
  computed: {
    className: function() {
      var name = this.labelName.replace(" ", "");
      return name;
    }
  },
  methods: {
    changedValue: function(e) {
      this.$emit("valueChanged", e.target.value);
    },
    focusBubble() {
      this.$emit("gotFocus");
    }
  }
};
</script>
