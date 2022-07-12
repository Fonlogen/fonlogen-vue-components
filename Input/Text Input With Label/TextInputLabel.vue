<script>

export default {
  data() {
    return {
      isHovering: false,
    }
  },

  props: {
    label: {
      type: String,
      required: true
    },
    /*
    The type of the input.
    Must be: 
    - text
    - password
    - email
    - number
    - date
    */
    inputType: {
      type: String,
      required: false,
      default: 'text'
    },
    placeholder: {
      type: String,
      required: false,
      default: ''
    },
    value: {
      type: String,
      required: false,
      default: ''
    },
  },

  methods: {
    toggleHover(e) {
      this.isHovering = !this.isHovering;

      var hover_color = getComputedStyle(document.documentElement).getPropertyValue('--hover-border-color');
      //var default_color = getComputedStyle(document.documentElement).getPropertyValue('--input-text-color');
      var input_border_color = getComputedStyle(document.documentElement).getPropertyValue('--input-border-color');

      if (this.isHovering) {
        this.$refs['input_label'].style.color = hover_color;
        e.target.style.borderColor = hover_color;
      } else {
        this.$refs['input_label'].style.color = input_border_color;
        e.target.style.borderColor = input_border_color;
      }
    }
  }
}

</script>

<template>
  <div className="text-input-label">
    <label ref="input_label">{{label}}</label>
    <input 
      v-on:mouseover="toggleHover"
      v-on:mouseleave="toggleHover"
      ref="input_area" 
      :type="inputType" 
      :placeholder="placeholder" />
  </div>
</template>

<style>





:root {
  --bg-color: #232323;
  --input-border-color: #8f8c8c;
  --input-text-color: white;
  --label-text-color: var(--input-border-color);


  --hover-border-color: rgb(118, 106, 200);
}

.text-input-label {
  position: relative;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  padding: 5px 5px;
}

.text-input-label label {
  font-size: 0.8em;
  position: absolute;
  color: var(--label-text-color);
  background-color: var(--bg-color);
  padding: 0 5px;
  border-radius: 0.75rem;
  top: 5px;
  left: 15px;
  pointer-events: none;
}

.text-input-label input {
  color: var(--input-text-color);
  width: 250px;
  font-size: 1.2em;
  padding: 12px 30px;
  border: 1.5px solid #666565;
  border-radius: 15px;
  background-color: var(--bg-color);
  text-align: center;
  margin-top: 10px;
  margin-bottom: 10px;
}

.text-input-label input:focus {
  border-color: var(--hover-border-color);
  border-width: 2px;
  outline: none;
}

</style>