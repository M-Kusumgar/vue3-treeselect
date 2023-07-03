<script>
  import { defineComponent } from 'vue'
  import Input from './Input'
  import Placeholder from './Placeholder'

  export default defineComponent({
    name: 'vue-treeselect--single-value',
    inject: [ 'instance' ],
    methods: {
      renderSingleValueLabel() {
        const { instance } = this
        const node = instance.selectedNodes[0]

        const customValueLabelRenderer = instance.$slots['value-label']

        if (customValueLabelRenderer) {
          return customValueLabelRenderer({ node })
        } else {
          return node?.label || null
        }
      },
    },
    render() {
      const { instance, $parent: { renderValueContainer } } = this
      const shouldShowValue = instance.hasValue && !instance.trigger.searchQuery

      return renderValueContainer([
        shouldShowValue && (
          <div class="vue-treeselect__single-value">
            { this.renderSingleValueLabel() }
          </div>
        ),
        <Placeholder />,
        <Input ref="input" />,
      ])
    },
  })
</script>
