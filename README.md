# AzureDevOps-dedicatedSQLPoolToFabricDW
Example of a state-Based deployment that can create a dacpac file based on an existing database within a dedicated SQL Pool and then deploy it to a Microsoft Fabric Data Warehouse.

It is based on a blog post I wrote called Migrate dedicated SQL Pool objects to a Microsoft Fabric Data Warehouse.

You can find the YAML file which you can use as a template for the Azure Pipeline in the AzureDevOpsTemplates folder. 

Note that you need a recent version of SQLPackage for this to work.

The '[dedicatedSQLPool-sqlpackage.yml pipeline](https://github.com/kevchant/AzureDevOps-dedicatedSQLPoolToFabricDW/blob/main/AzureDevOpsTemplates/dedicatedSQLPool-sqlpackage.yml)' extracts the contents of a database in a dedicated SQL Pool to a dacpac. It then deploys the contents of the dacpac to a Microsoft Fabric Data Warehouse.

Please note that you need the below variables created for this YAML pipeline to work:
I recommend doing this by creating at least one variable group
*   agentpool - The name of the agent pool you want to use (ideally a self-hosted one with latest sqlpackage installed).
     Otherwise you must put additional logic in this pipeline to deploy latest version of sqlpackage onto the agent
*   TargetFile - The name of the dacpac that you want to be created
*   TargetFolder - The name of the Folder the Azure Pipelines works with behind the scenes
*   SourceSQLPoolEndPoint - The name of your serverless SQL Pool endpoint (which you can get in the Azure Synapse overview)
*   SourceDB - The name of database in the serverless SQL Pool you want to extract the schema from
*   SQLPooluser - A SQL login that can access the serverless SQL Pool
*   SQLPoolpw - The p/w for the above SQL login
*   SQLPoolartifactname - A name for the created artifact
*   AzureSubscription - The Azure subscription that contains the Azure Active Directory tenant used by your Microsoft Fabric environment
*   aadSqlUsername - An Azure Active Directory account
*   aadSqlpw - P/w for the Azure Active Directory account
*   DestSQLConnString - The connection string used by the Microsoft Fabric Data Warehouse. As shown '[here](https://learn.microsoft.com/en-us/fabric/data-warehouse/connectivity)'
*   DestinationDW - The name of your Microsoft Fabric Data Warehouse


Note that you can extend this however you see fit.

