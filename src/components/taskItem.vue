<template>
  <div class="task task--dark" :class="{ 'text--completed': completed }">
    <div
      :onclick="() => this.$emit('onChangeTaskStatus', id, !completed)"
      class="check check--dark"
    >
      <svg
        v-if="completed"
        xmlns="http://www.w3.org/2000/svg"
        viewBox="0 0 65 49.49"
      >
        <title>check</title>
        <g id="Ebene_2" data-name="Ebene 2">
          <g id="check">
            <g id="Page-1">
              <g id="Core">
                <g id="check-2" data-name="check">
                  <path
                    id="Shape"
                    class="cls-1"
                    d="M20.68,39.15,5.17,23.64,0,28.81,20.68,49.49,65,5.17,59.83,0Z"
                  />
                </g>
              </g>
            </g>
          </g>
        </g>
      </svg>
    </div>
    <p class="text text--dark" :class="{ 'text--completed': completed }">
      {{ title }}
    </p>
    <svg
      :onclick="() => this.$emit('onDelete')"
      xmlns="http://www.w3.org/2000/svg"
      viewBox="0 0 65 65"
    >
      <title>close</title>
      <g id="Ebene_2" data-name="Ebene 2">
        <g id="close">
          <path
            d="M65,6.57,58.43,0,32.5,25.93,6.57,0,0,6.57,25.93,32.5,0,58.43,6.57,65,32.5,39.07,58.43,65,65,58.43,39.07,32.5Z"
          />
        </g>
      </g>
    </svg>
  </div>
</template>

<script>
export default {
  name: "task-item",

  props: {
    completed: {
      type: Boolean,
      default: true,
      required: true,
    },
    title: {
      type: String,
      default: "",
      required: true,
    },
  },

  methods: {},
};
</script>
