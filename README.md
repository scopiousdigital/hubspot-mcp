# HubSpot MCP Server

MCP Server for the HubSpot API, enabling Claude to interact with HubSpot CRM for sales analysis and insights.

> #### Disclaimer
>
> This open-source project is not affiliated with or endorsed by HubSpot. It is an independent implementation that interacts with HubSpot's API.

## Tools

### Core CRM Tools

1. `hubspot_search_contacts`

   - Search for contacts in HubSpot using a query string
   - Required inputs:
     - `query` (string): Search query string (email, name, etc.)
   - Optional inputs:
     - `count` (number, default: 10): Maximum number of contacts to return
     - `propertyList` (array): List of properties to include in results
   - Returns: List of matching contacts with their properties

2. `hubspot_get_contact`

   - Get a specific contact by ID
   - Required inputs:
     - `contactId` (string): The ID of the contact to retrieve
   - Optional inputs:
     - `properties` (array): List of properties to include in results
   - Returns: Contact details with specified properties

3. `hubspot_create_contact`

   - Create a new contact in HubSpot
   - Required inputs:
     - `properties` (object): Contact properties with at least `email` field
   - Returns: Created contact details

4. `hubspot_update_contact`

   - Update an existing contact in HubSpot
   - Required inputs:
     - `contactId` (string): The ID of the contact to update
     - `properties` (object): Contact properties to update
   - Returns: Updated contact confirmation

5. `hubspot_list_deals`

   - List deals in HubSpot with pagination
   - Optional inputs:
     - `limit` (number, default: 10, max: 100): Maximum number of deals to return
     - `after` (string): Pagination cursor for next page
     - `properties` (array): List of properties to include in results
   - Returns: List of deals with their details

6. `hubspot_get_deal`

   - Get a specific deal by ID
   - Required inputs:
     - `dealId` (string): The ID of the deal to retrieve
   - Optional inputs:
     - `properties` (array): List of properties to include in results
   - Returns: Deal details with specified properties

7. `hubspot_create_deal`

   - Create a new deal in HubSpot
   - Required inputs:
     - `properties` (object): Deal properties with at least `dealname` field
   - Returns: Created deal details

8. `hubspot_update_deal`

   - Update an existing deal in HubSpot
   - Required inputs:
     - `dealId` (string): The ID of the deal to update
     - `properties` (object): Deal properties to update
   - Returns: Updated deal confirmation

9. `hubspot_list_companies`

   - List companies in HubSpot with pagination
   - Optional inputs:
     - `limit` (number, default: 10, max: 100): Maximum number of companies to return
     - `after` (string): Pagination cursor for next page
     - `properties` (array): List of properties to include in results
   - Returns: List of companies with their details

10. `hubspot_get_company`
    - Get a specific company by ID
    - Required inputs:
      - `companyId` (string): The ID of the company to retrieve
    - Optional inputs:
      - `properties` (array): List of properties to include in results
    - Returns: Company details with specified properties

### Sales Analytics Tools

11. `hubspot_get_sales_analytics`

    - Get aggregated sales analytics data for specific time periods
    - Required inputs:
      - `period` (string): Time period to group analytics data by (daily, weekly, monthly, quarterly, yearly)
      - `startDate` (string): Start date for analysis in ISO format (YYYY-MM-DD)
    - Optional inputs:
      - `endDate` (string): End date for analysis in ISO format
      - `pipeline` (string): Pipeline ID to filter by
      - `dealStage` (string): Deal stage ID to filter by
      - `dealOwner` (string): Deal owner ID to filter by
    - Returns: Aggregated sales metrics grouped by time period

12. `hubspot_get_deal_history`

    - Get the complete history of changes to a deal
    - Required inputs:
      - `dealId` (string): The ID of the deal to get history for
    - Returns: History of deal changes with timestamps and modified properties

13. `hubspot_get_deal_notes`

    - Get notes associated with a specific deal
    - Required inputs:
      - `dealId` (string): The ID of the deal to get notes for
    - Optional inputs:
      - `limit` (number, default: 20): Maximum number of notes to return
      - `after` (string): Pagination cursor for next page of results
    - Returns: List of notes with their content and creation timestamps

14. `hubspot_get_engagements_by_deal`

    - Get all engagement activities associated with a deal
    - Required inputs:
      - `dealId` (string): The ID of the deal to get engagements for
    - Optional inputs:
      - `types` (array): Types of engagements to include (CALL, EMAIL, MEETING, TASK, NOTE)
      - `limit` (number, default: 20): Maximum number of engagements to return
      - `after` (string): Pagination cursor for next page of results
    - Returns: List of engagements with their details and type information

15. `hubspot_get_sales_performance`

    - Get performance metrics for sales reps over a specific time period
    - Required inputs:
      - `period` (string): Time period to group performance data by (daily, weekly, monthly, quarterly, yearly)
      - `startDate` (string): Start date for analysis in ISO format (YYYY-MM-DD)
    - Optional inputs:
      - `endDate` (string): End date for analysis in ISO format
      - `ownerIds` (array): List of owner IDs to include in the analysis
      - `pipeline` (string): Pipeline ID to filter by
    - Returns: Performance metrics for each sales rep including deal counts, revenue, and win rates

16. `hubspot_get_pipeline_analytics`

    - Get analytics for a specific sales pipeline including conversion rates between stages
    - Required inputs:
      - `pipelineId` (string): The ID of the pipeline to analyze
      - `period` (string): Time period to group analytics data by (daily, weekly, monthly, quarterly, yearly)
      - `startDate` (string): Start date for analysis in ISO format (YYYY-MM-DD)
    - Optional inputs:
      - `endDate` (string): End date for analysis in ISO format
    - Returns: Pipeline stage metrics including deal counts, values, conversion rates, and time in stage

17. `hubspot_get_forecast_analytics`
    - Get forecasted sales data based on current pipeline and historical performance
    - Required inputs:
      - `period` (string): Time period to group forecast data by (monthly, quarterly, yearly)
    - Optional inputs:
      - `numberOfPeriods` (number, default: 3): Number of future periods to forecast
      - `pipeline` (string): Pipeline ID to filter by
    - Returns: Forecasted sales metrics for future periods based on historical data and current pipeline

## Setup

1. Create a HubSpot Private App:

   - Go to your HubSpot account
   - Navigate to Settings → Account Setup → Integrations → Private Apps
   - Click "Create private app"
   - Name your app and set appropriate scopes (contacts, deals, and companies)
   - Create the app and copy your private app token

2. Required Scopes:
   - `crm.objects.contacts.read`
   - `crm.objects.contacts.write`
   - `crm.objects.deals.read`
   - `crm.objects.deals.write`
   - `crm.objects.companies.read`
   - `crm.objects.companies.write`
   - `crm.objects.owners.read`
   - `crm.objects.quotes.read`
   - `crm.objects.line_items.read`
   - `crm.objects.custom.read`
   - `crm.schemas.deals.read`
   - `crm.schemas.contacts.read`
   - `crm.schemas.companies.read`
   - `crm.schemas.custom.read`

### Usage with Claude Desktop

Add the following to your `claude_desktop_config.json`:

#### npx

```json
{
  "mcpServers": {
    "hubspot": {
      "command": "npx",
      "args": ["-y", "@scopiousdigital/server-hubspot"],
      "env": {
        "HUBSPOT_API_KEY": "your-api-key-here"
      }
    }
  }
}
```

#### docker

```json
{
  "mcpServers": {
    "hubspot": {
      "command": "docker",
      "args": ["run", "-i", "--rm", "-e", "HUBSPOT_API_KEY", "mcp/hubspot"],
      "env": {
        "HUBSPOT_API_KEY": "your-api-key-here"
      }
    }
  }
}
```

### Troubleshooting

If you encounter errors, verify that:

1. All required scopes are added to your HubSpot private app
2. The API key is correctly copied to your configuration
3. Your HubSpot plan includes access to the APIs you're trying to use

## Build

Docker build:

```bash
docker build -t mcp/hubspot -f Dockerfile .
```

## License

This MCP server is licensed under the MIT License. This means you are free to use, modify, and distribute the software, subject to the terms and conditions of the MIT License. For more details, please see the LICENSE file in the project repository.

Maintained by [Scopious Digital](https://www.scopiousdigital.com/?utm_source=github&utm_medium=readme&utm_campaign=hubspot-mcp). We build HubSpot integrations and white-label dev for HubSpot agencies.
