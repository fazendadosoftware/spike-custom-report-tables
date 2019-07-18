<template>
  <div id="app">
    Spike: Custom Report Tables
  </div>
</template>

<script>

export default {
  name: 'app',
  created () {
    this.$lx.init()
      .then(setup => {
        const reportConfiguration = {
          allowTableView: true,
          // This callback is invoked whenever the user switches to the table config mode. It should provide a reasonable default for the initial configuration of the table.
          // Reference: https://leanix.github.io/leanix-reporting/interfaces/lxr.reporttableconfig.html
          tableConfigCallback: () => {
            return {
              attributes: [
                { key: 'id', label: 'FactSheet ID' },
                'type', // attribute can be also a string
                { key: 'name', label: 'FactSheet Name' },
                { key: 'lifecycle', label: 'Lifecycle: plan', type: 'LIFECYCLE', virtualKey: 'plan', isCustomColumn: false },
                { key: 'lifecycle', label: 'Lifecycle: phase in', type: 'LIFECYCLE', virtualKey: 'phaseIn', isCustomColumn: false },
                { key: 'lifecycle', label: 'Lifecycle: active', type: 'LIFECYCLE', virtualKey: 'active', isCustomColumn: false },
                { key: 'lifecycle', label: 'Lifecycle: phase out', type: 'LIFECYCLE', virtualKey: 'phaseOut', isCustomColumn: false },
                { key: 'lifecycle', label: 'Lifecycle: end of life', type: 'LIFECYCLE', virtualKey: 'endOfLife', isCustomColumn: false }
              ]
            }
          },
          facets: [
            {
              key: 'businessCapability',
              label: 'Business Capabilities',
              fixedFactSheetType: 'BusinessCapability',
              attributes: ['id', 'name', '...on BusinessCapability{lifecycle{phases{phase startDate}}}'],
              callback: dataset => {
                console.log('BUSINESS CAPABILITIES', dataset)
              }
            }
          ]
        }
        this.$lx.ready(reportConfiguration)
        setTimeout(() => {
          console.log('TABLE', this.$lx.table)
        })
      })
  }
}
</script>
