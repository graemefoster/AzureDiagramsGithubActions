# AzureDiagrams

## Generate a Draw.IO diagram from your Azure Resources

### Github Action

Here's an example that:

- Uses the Custom Github Action to generate a draw.io diagram
- Uploads the diagram as an artifact in your action.

```yaml
      - uses: azure/login@v1
        with:
          creds: ${{ secrets.AZURE_CREDENTIALS }}

      - name: Generate Diagram
        uses: graemefoster/azurediagramsgithubactions@v0.1.10
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
| outputFileName    | Yes       | Filename to write Draw.Io output                                             |
| accessToken       | No        | Optional JWT to avoid using CLI credential                                   |
| condensed         | No        | True collapses private endpoints into subnets (can simplify large diagrams)  |
| showRuntime       | No        | True to show runtime flows defined on the control plane                      |
| showInferred      | No        | True to infer connections between resources by introspecting appSettings     |
| showIdentity      | No        | True to show User Assigned Managed Identity connections                      |
| showDiagnostics   | No        | True to show diagnostics flows                                               |

## Output Formats
The initial version supports Draw.IO diagrams. 
