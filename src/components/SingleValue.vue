<script>
  import { defineComponent } from 'vue'
import Input from './Input'
  import Placeholder from './Placeholder'

  export default defineComponent({
    name: 'vue-treeselect--single-value',
    inject: [ 'instance' ],
    data() {
      return {
        singleValue: ""
      }
    },
    methods: {
      renderSingleValueLabel() {
        const { instance } = this
        const node = instance.selectedNodes[0]

        const customValueLabelRenderer = instance.$slots['value-label']

        if (customValueLabelRenderer) {
          this.singleValue = customValueLabelRenderer({ node })
        } else {
          this.singleValue = node?.label || ""
        }
      },
    },
    computed: {
      nodeLabel() {
        const { instance } = this
        const node = instance.selectedNodes[0]
        return node?.label
      }
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
    watch: {
      nodeLabel: {
        handler: function (newNode) {
          this.renderSingleValueLabel()
        },
        deep: true
      }
    }
  })
</script>
