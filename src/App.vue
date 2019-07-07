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
                { key: 'id', label: 'FactSheet ID', sortable: true },
                { key: 'type', label: 'FactSheet Type', sortable: false },
                { key: 'name', label: 'FactSheet Name', sortable: false }
              ]
            }
          },
          facets: [
            {
              key: 'businessCapability',
              label: 'Business Capabilities',
              fixedFactSheetType: 'BusinessCapability',
              attributes: ['id', 'name'],
              callback: dataset => {
                console.log('APPLICATIONS', dataset)
              }
            },
            {
              key: 'applications',
              label: 'Applications',
              fixedFactSheetType: 'BusinessCapability',
              attributes: ['id', 'name'],
              callback: dataset => {
                console.log('BUSINESS CAPABILITIES', dataset)
              }
            }
          ]
        }
        this.$lx.ready(reportConfiguration)
      })
  }
}
</script>
