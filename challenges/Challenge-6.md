# Implement a monitoring solution for your MyDriving APIs

**Resist the initial temptation to rush on the keyboard! This is the time to pause and think as a team about your end-to-end deployment process that you would implement in this company.**

**Reminders:**

- Use an InPrivate/Incognito window in your browser to avoid any confusion with any other credentials that you may use to access Azure resources.

--------------

With a functional pipeline that builds and deploys your APIs, your next step is to focus on their health and performance.

## Challenge

Your challenge is to define and implement a monitoring strategy for your APIs.

Carefully select the monitoring tool(s) that you want to use.

You are expected to achieve the following goals:

- Implement a solution that monitors the health and performance of your APIs. You will have to collect data regarding the performance of your web applications and the APIs hosted in each web application.
- Define the performance baseline for the APIs running in Azure and implement a mechanism that will automatically raise an alert and create an incident in your work item tracking system if a performance degradation is observed.
- Build a dashboard that will allow you to visualize the global health of your environment.

> **Note:** It is recommended to discuss the capabilities of the tools that you have selected with your team. Keep in mind that your coach is here to help you make an educated decision.

## Success Criteria

Show your coach the aggregated view of your application and infrastructure that includes the following:

- Web application monitoring that displays the CPU utilization for each production web application
- The average response time over a period of 1 minute for each production web application
- A work item is created when API performance degradation is observed
- The top 10 queries by duration over the last 24 hours for the **mydrivingDB** database
- The percentage of DTU utilized on the **mydrivingDB** database

Show to your coach that an incident is automatically created when an alert is raised.

## References

### Azure resources

- **Azure Monitor**
    - <a href="https://docs.microsoft.com/azure/azure-monitor/overview" target="blank">Overview of the Azure Monitoring solutions</a>
    - <a href="https://docs.microsoft.com/azure/azure-monitor/log-query/get-started-portal" target="_blank">Getting started with Azure Monitor Log Analytics</a>
    - <a href="https://docs.microsoft.com/azure/azure-monitor/insights/monitor-azure-resource" target="_blank">Monitoring Azure resources with Azure Monitor</a>
    - <a href="https://docs.microsoft.com/azure/azure-monitor/app/azure-web-apps" target="_blank">Monitor Azure App Service performance</a>
    - <a href="https://docs.microsoft.com/azure/azure-monitor/insights/azure-sql" target="_blank">Monitor Azure SQL Database using Azure SQL Analytics</a>
    - <a href="https://docs.microsoft.com/Azure/app-service/web-sites-monitor" target="_blank">Create diagnostic setting to collect resource logs and metrics in Azure</a>
    - <a href="https://docs.microsoft.com/azure/azure-monitor/platform/diagnostic-settings" target="_blank">Monitor apps in Azure App Service</a>
    - <a href="https://docs.microsoft.com/azure/azure-monitor/platform/diagnostic-settings" target="_blank">What is Application Insights?</a>
    - <a href="https://docs.microsoft.com/azure/azure-monitor/platform/alerts-log" target="_blank">Create, view, and manage log alerts using Azure Monitor</a>
    - <a href="https://docs.microsoft.com/azure/azure-monitor/platform/alerts-overview" target="_blank">Overview of alerts in Microsoft Azure</a>
- **Azure Logic Apps**
    - <a href="https://docs.microsoft.com/azure/logic-apps/logic-apps-overview" target="_blank">Overview - What is Azure Logic Apps?</a>
    - <a href="https://docs.microsoft.com/connectors/visualstudioteamservices/" target="_blank">Azure DevOps Connector for Azure Logic Apps</a>
- **Kusto documentation and references**:
    - The solutions in Azure will evolve to use <a href="https://docs.microsoft.com/azure/kusto/query/" target="_blank">Azure Data Explorer query language</a> (also know as <a href="https://docs.microsoft.com/azure/kusto/query/" target="_blank">Kusto</a>)
    - Syntax for regular expressions supported by <a href="https://docs.microsoft.com/azure/kusto/query/re2" target="_blank">Azure Data Explorer</a>
- **Regular Expressions**
    - You can test your regular expression on this site: <a href="https://regexr.com/" target="_blank">RegExr: Learn, Build, & Test RegEx</a>
    - You can use regular expressions in the `extract()` function in Kusto. For example, this code will extract and convert to a double the response time from the container output showed above:

        ```sh
        todouble(extract(@"CreateTripPoint ([0-9.]*)ms", 1, LogEntry))
        ```

- **Application availability and responsiveness**
    - <a href="https://docs.microsoft.com/azure/azure-monitor/app/monitor-web-app-availability#alerts" target="_blank">Availability alerts of any web site</a>

### Additional Reading

- <a href="https://docs.microsoft.com/azure/azure-monitor/overview" target="_blank">Azure Monitor overview</a>
- <a href="https://docs.microsoft.com/azure/app-service/faq-availability-performance-application-issues" target="_blank">Application performance FAQs for Web Apps in Azure</a>
