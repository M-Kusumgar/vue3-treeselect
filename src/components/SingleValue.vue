<script>
  import Input from './Input'
  import Placeholder from './Placeholder'

  export default {
    name: 'vue-treeselect--single-value',
    inject: [ 'instance' ],
    data() {
      singleValue: ""
    },
    methods: {
      renderSingleValueLabel() {
        const { instance } = this
        const node = instance.selectedNodes[0]

        const customValueLabelRenderer = instance.$slots['value-label']
        this.singleValue = customValueLabelRenderer
          ? customValueLabelRenderer({ node })
          : node.label
      },
    },
    render() {
      const { instance, $parent: { renderValueContainer } } = this
      const shouldShowValue = instance.hasValue && !instance.trigger.searchQuery

      return renderValueContainer([
        shouldShowValue && (
          <div class="vue-treeselect__single-value">
            { this.singleValue }
          </div>
        ),
        <Placeholder />,
        <Input ref="input" />,
      ])
    },
    mounted() {
      this.renderSingleValueLabel()
    },
    updated() {
      this.renderSingleValueLabel()
    }
  }
</script>
