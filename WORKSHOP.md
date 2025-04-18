# Use `GitHub Copilot app modernization for Java on Azure` to migrate this project

> [!IMPORTANT]
> `GitHub Copilot app modernization for Java on Azure` is in preview and is subject to change before becoming generally available.

`GitHub Copilot app modernization for Java on Azure` assists with app assessment, planning and code remediation. It automates repetitive tasks, boosting developer confidence and speeding up the Azure migration and ongoing optimization.

In this workshop, you learn how to use `GitHub Copilot app modernization for Java on Azure` to assess and migrate a sample Java application `asset-manager` to Azure. For more information about the sample application, see [Asset Manager](README.md).

## Prerequisites

To successfully complete this workshop, you need the following:

- [VSCode](https://code.visualstudio.com/): The latest version is recommended.
- [A Github account with Github Copilot enabled](https://github.com/features/copilot): All plans are supported, including the Free plan.
- [GitHub Copilot extension in VSCode](https://code.visualstudio.com/docs/copilot/overview): The latest version is recommended.
- [AppCAT](https://aka.ms/appcat-install): Required for the app assessment feature.
- [JDK 21](https://learn.microsoft.com/en-us/java/openjdk/download#openjdk-21): Required for the code remediation feature and running the initial application locally.
- [Maven 3.9.9](https://maven.apache.org/install.html): Required for the code remediation feature.
- [Azure subscription](https://azure.microsoft.com/free/): Required to deploy the migrated application to Azure.
- [Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli): Required if you deploy the migrated application to Azure locally. The latest version is recommended.
- Fork the [GitHub repository](https://github.com/Azure-Samples/java-migration-copilot-samples) that contains the sample Java application. **MAKE SURE TO UNCHECK THE BOX "Copy the `main` branch only.** Clone it to your local machine. Open the `asset-manager` folder in VSCode and checkout the `workshop` branch.

## Install GitHub Copilot app modernization for Java on Azure Tool

In VSCode, open the Extensions view from Activity Bar, search `GitHub Copilot app modernization for Java on Azure` extension in marketplace. Select the Install button on the extension. After installation completes, you should see a notification in the bottom-right corner of VSCode confirming success.


## Migrate the Sample Java Application

The following sections guide you through the process of migrating the sample Java application `asset-manager` to Azure using GitHub Copilot app modernization for Java on Azure.

### Assess Your Java Application

The first step is to assess the sample Java application `asset-manager`. The assessment provides insights into the application's readiness for migration to Azure.

1. Open the VS code with all the prerequisites installed on the asset manager by changing the directory to the `asset manager` directory and running `code .` in that directory.
1. Open the extension `GitHub Copilot app modernization for Java on Azure`.
1. The **Assess** button looks a triangle pointing right. Select **Assess**, the Github Copilot chat window will be opened and propose to run Modernization Assessor. Please confirm the tool usage by clicking **Continue**. 

   > **NOTE**: If you are asked to allow the tool access the language models provided by GitHub Copilot Chat, slect **Allow** to proceed.

1. Wait for the assessment to be completed and the report to be generated.
1. Review the **Summary** report. Select **Propose Solution** to view the proposed solutions for the issues identified in the summary report.
1. For this workshop, deselect all solutions and select **Use Azure Database for PostgreSQL** in the Solution report, then select **Confirm Solution**.
1. In the Migrate report, click **Migrate**.

### Migrate to Azure Database for PostgreSQL Flexible Server using Predefined Formula

1. In Copilot chat window, scroll to the bottom in the Copilot Chat window.
1. In the GitHub Copilot Chat pane, scroll to the bottom to view the list of available formulas.
1. Select the predefined formula for **Azure Database for PostgreSQL Flexible Server**.
1. Click **Continue** repeatedly to confirm each tool action.
1. Review the proposed code changes and click **Keep** to apply them.
1. Click **Continue** to confirm to run **Java Application Build-Fix** tool. This tool will attempt to resolve any build errors, in up to 10 iterations.
1. After the Build-Fix tool begins, click **Continue** to proceed and show progress and migration summary.

### Migrate to Azure Blob Storage and Azure Service Bus using Custom Formula

Recall that the sample Java application `asset-manager` uses AWS S3 for image storage and Spring AMQP RabbitMQ for message queuing. The `workshop` branch has additional commits that have already migrated the code for **Web Application** with custom code remediation to use Azure Blob Storage and Azure Service Bus, respectively. 

Now, you migrate the **Worker Service** to use Azure Blob Storage and Azure Service Bus as well, by using custom formula created from existing commits that migrated the **Web Application**.

1. Open the sidebar of `GitHub Copilot app modernization for Java on Azure`. Hover the mouse over the **Formulas** section.  Select **Create formula from source control**. This icon looks like two circles with arrows pointing to the other circle. Type **migrate web** to search for the commits that migrated the **Web Application**, and you should see two commits listed:
   * migrate web rabbitmq to azure service bus
   * migrate web s3 to azure blob storage
1. Select these two commits. Click **Create New** to create a new custom formula.
1. Formula name, formula description, and code location patterns will be generated in order. Press `Enter` repeatedly to confirm.
1. Select and run the custom formula you created in the FORMULAS section of the sidebar of `GitHub Copilot app modernization for Java on Azure`. Follow the same steps as the predefined formula to review and apply the changes, and run the **Java Application Build-Fix** tool to apply build fixes.

## Deploy to Azure

At this point, you have successfully migrated the sample Java application `asset-manager` to use Azure Database for PostgreSQL, Azure Blob Storage, and Azure Service Bus. Now, you deploy the migrated application to Azure using the Azure CLI after you identify a working location for your Azure resources.

For example, an Azure Database for PostgreSQL Flexible Server requires a location that supports the service. Follow the instructions below to find a suitable location.

1. Run the following command to list all available locations for your account:

   ```bash
   az account list-locations -o table
   ```

1. Try a location from column **Name** in the output. For example, `eastus2` stands for **East US 2**.

1. Run the following command to list all available SKUs in the selected location for Azure Database for PostgreSQL Flexible Server:

   ```bash
   az postgres flexible-server list-skus --location <your location> -o table
   ```

1. If you see the output contains the SKU `Standard_B1ms` and the **Tier** is `Burstable`, you can use the location for the deployment. Otherwise, try another location.

   ```text
   SKU                Tier             VCore    Memory    Max Disk IOPS
   -----------------  ---------------  -------  --------  ---------------
   Standard_B1ms      Burstable        1        2 GiB     640e
   ```

You can either run the deployment script locally or use the GitHub Codespaces. The recommended approach is to run the deployment script in the GitHub Codespaces, as it provides a ready-to-use environment with all the necessary dependencies.

Deploy using GitHub Codespaces:
1. Commit and push the changes to your forked repository.
1. Follow instructions in [Use GitHub Codespaces for Deployment](README.md#use-github-codespaces-for-deployment) to deploy the app to Azure.

Deploy using local environment by running the deployment script in the terminal:
1. Run `az login` to sign in to Azure.
1. Run the following commands to deploy the app to Azure:
   
   Winndows:
   ```batch
   scripts\deploy-to-azure.cmd -ResourceGroupName <your resource group name> -Location <your resource group location, e.g., eastus2> -Prefix <your unique resource prefix>
   ```

   Linux:
   ```bash
   scripts/deploy-to-azure.sh -ResourceGroupName <your resource group name> -Location <your resource group location, e.g., eastus2> -Prefix <your unique resource prefix>
   ```

Once the deployment script completes successfully, it outputs the URL of the Web application. Open the URL in a browser to verify if the application is running as expected.

## Clean up

When you are done with the workshop, clean up the Azure resources to avoid incurring costs.

Winndows:
```batch
scripts\cleanup-azure-resources.cmd -ResourceGroupName <your resource group name>
```

Linux:
```bash
scripts/cleanup-azure-resources.sh -ResourceGroupName <your resource group name>
```

If you deploy the app using GitHub Codespaces, delete the Codespaces environment by navigating to your forked repository in GitHub and selecting **Code** > **Codespaces** > **Delete**.
