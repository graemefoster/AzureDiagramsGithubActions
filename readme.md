# AzureDiagrams

## Generate a Draw.IO diagram from your Azure Resources

### Github Action

First, run az login

Here's an example that:
- use the Custom Github Action to generate a draw.io diagram
- publish the diagram as an artefact.


```yaml
      - uses: azure/login@v1
        with:
          creds: ${{ secrets.AZURE_CREDENTIALS }}

      - name: Generate Diagram
        uses: graemefoster/azurediagramsgithubactions@v0.1.1
        with:
          subscriptionId: ${{ secrets.AZURE_SUBSCRIPTION_ID }}
          resourceGroup: "*-grf-*"
          outputFileName: "azurediagram.drawio"

      - uses: actions/upload-artifact@v3
        with:
          name: diagram
          path: ./azurediagram.drawio
```
## Yaml properties

| Property          | Required  | Description                                                                  |
|:------------------|:----------|:-----------------------------------------------------------------------------|
| subscriptionId    | Yes       | Subscription Id to run against                                               |
| resourceGroup     | Yes       | Wildcard enabled resource group name (supports multiple)                     |
| accessToken       | Yes       | Optional JWT to avoid using CLI credential                                   |
| condensed         | Yes       | True collapses private endpoints into subnets (can simplify large diagrams)  |
| showRuntime       | Yes       | True to show runtime flows defined on the control plane                      |
| showInferred      | Yes       | True to infer connections between resources by introspecting appSettings     |
| showIdentity      | Yes       | True to show User Assigned Managed Identity connections                      |
| showDiagnostics   | Yes       | True to show diagnostics flows                                               |
| outputPng         | Yes       | True to export a png of the draw.io diagram                                  |


## Output Formats
The initial version supports Draw.IO diagrams. 
