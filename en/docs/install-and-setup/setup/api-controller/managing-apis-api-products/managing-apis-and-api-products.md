# Managing APIs and API Products

## Add APIs or API Products in an environment

You can add APIs and API Products via the Publisher Portal.
However, **WSO2 API Controller (apictl)** allows you to create and deploy APIs without using the Publisher Portal. For more information on adding APIs, see [Importing APIs Via Dev First Approach]({{base_path}}/install-and-setup/setup/api-controller/managing-apis-api-products/importing-apis-via-dev-first-approach).

## Get APIs or API Products in an environment

Follow the instructions below to display a list of APIs or API Products in an environment using apictl:

1.  Make sure that the WSO2 API Manager is started and the apictl is set up.   
     For more information, see [Download and Initialize the apictl]({{base_path}}/install-and-setup/setup/api-controller/getting-started-with-wso2-api-controller/#download-and-initialize-the-apictl).
2.  Log in to the WSO2 API-M in the environment by following the instructions in [Login to an Environment]({{base_path}}/install-and-setup/setup/api-controller/getting-started-with-wso2-api-controller/#login-to-an-environment).
3.  Run the corresponding apictl command below to get (list) APIs or API Products in an environment.

    1. Get APIs in an environment.

        -   **Command**
            ``` bash
            apictl get apis -e <environment>
            ```
            ``` bash
            apictl get apis --environment <environment>
            ```
            ``` bash
            apictl get apis --environment <environment> --query <API search query> 
            ```

            !!! info
                **Flags:**  
                
                -   Required :  
                    `--environment` or `-e` : Environment to be searched  
                -   Optional :  
                    `--query` or `-q` : Search query pattern  
                    `--limit` or `-l` : Maximum number of APIs to return (Default 25)
                    `--format` : pretty-print APIs using Go templates

            !!! example
                ```bash
                apictl get apis -e dev 
                ```
                ```bash
                apictl get apis --environment production --limit 15 
                ```    
                ```go
                apictl get apis --environment production --query provider:Alice --query name:PizzaShackAPI version:2.0.0 
                ```  

        -   **Response**

            ```go
            ID                                     NAME                VERSION             CONTEXT             STATUS              PROVIDER
            12d6e73c-778d-45ac-b57d-117c6c5092a4   PhoneVerification   1.0                 /phoneverify        PUBLISHED           admin
            91fe87c3-f0d7-4c35-81f5-0e0e42d8e19f   PizzaShackAPI       2.0.0               /pizzashack         CREATED             Alice
            ```
            
            !!! tip 
                When using the `apictl get apis -e dev` command, `-q` or `--query` optional flag can be used to 
                search for APIs.
                You can search in attributes by using a `:` modifier. Supported attribute modifiers are **name**, 
                **version**, **provider**, **context**, **status**, **description**, **subcontext** and **doc**. You can also use multiple modifiers specified by multiple `-q` or `--query` flags in the same command. When using multiple modifiers, make sure to separate them with space. 
                
                **Examples:**
                   
                -  `provider:wso2` will match an API if the provider of the API contains `wso2`.
                -  `'provider:"wso2"'` will match an API if the provider of the API is exactly `wso2`.
                -  `status:PUBLISHED` will match an API if the API is in PUBLISHED state.
                -  `name:pizzashack version:v1` will match an API if the name of the API is pizzashack and version is v1.
                
                If no advanced attribute modifier has been specified, the API names containing the search term will 
                be returned as a result.

            !!!note
                Output of the `get apis` and `get api-products` commands can be formatted with Go Templates. For more information on formatting the get commands, see [Formatting the outputs of get commands]({{base_path}}/install-and-setup/setup/api-controller/advanced-topics/formatting-the-output-of-get-command).

            !!!note
                `apictl list apis` command has been deprecated from apictl 4.0.0 onwards. Instead use `apictl get apis` as shown above. 

    2. Get API Products in an environment.
    
        -   **Command**
            ``` bash
            apictl get api-products -e <environment>
            ```
            ``` bash
            apictl get api-products --environment <environment>
            ```
            ``` bash
            apictl get api-products --environment <environment> --query <API search query>
            ```

            !!! info
                **Flags:**  
                
                -   Required :  
                    `--environment` or `-e` : Environment to be searched  
                -   Optional :  
                    `--query` or `-q` : Search query pattern  
                    `--limit` or `-l` : Maximum number of API Products to return
                    `--format` : pretty-print API Products using Go templates

            !!! example
                ```bash
                apictl get api-products -e dev 
                ```
                ```bash
                apictl get api-products --environment production 
                ```    
                ```go
                apictl get api-products --environment production --query provider:Alice name:CreditAPIProduct context:"/creditapiproduct" --limit 25 
                ```  

        -   **Response**

            ```go
            ID                                     NAME                  VERSION        CONTEXT              STATUS              PROVIDER
            b39e08d7-caa9-40d0-a430-b8e840dd7c31   LeasingAPIProduct     1.0.0          /leasingapiproduct   PUBLISHED           admin
            ab422af2-b19e-4e6a-a34b-8f45c50db0d5   CreditAPIProduct      2.1.0          /creditapiproduct    PUBLISHED           Alice
            ```

            !!!note
                `apictl list api-products` command has been deprecated from apictl 4.0.0 onwards. Instead use `apictl get api-products` as shown above.

## Get all revisions created for an API or API Product in an environment

Follow the instructions below to display a list of revisions created for an API or API Product in an environment using apictl:

1.  Make sure that the WSO2 API-M is started and the apictl is set up.   
     For more information, see [Download and Initialize the apictl]({{base_path}}/install-and-setup/setup/api-controller/getting-started-with-wso2-api-controller/#download-and-initialize-the-apictl).
2.  Log in to the WSO2 API-M in the environment by following the instructions in [Login to an Environment]({{base_path}}/install-and-setup/setup/api-controller/getting-started-with-wso2-api-controller/#login-to-an-environment).
3.  Run the corresponding apictl command below to get (list) revisions for the required API or API Product in an
 environment.

    1. Get revisions for an API in an environment.

        -   **Command**
            ``` bash
            apictl get api-revisions -n <API-name> -v <version> -e <environment> 
            ```
            ``` bash
            apictl get api-revisions --name <API-name> --version <version> --environment <environment>
            ```
            ``` bash
            apictl get api-revisions --name <API-name> --version <version> --provider <provider> --environment <environment> --query <deployment-search-query>
            ```

            !!! info
                **Flags:**  
                
                -   Required :  
                    `--name` or `-n` : Name of the API to get the revisions  
                    `--version` or `-v` : Version of the API to get the revisions  
                    `--environment` or `-e` : Environment to be searched  
                -   Optional :  
                    `--provider` or `-r` : Provider of the API  
                    `--query` or `-q` : Search query pattern  
                    `--format` : pretty-print API revisions using Go templates

            !!! example
                ```bash
                apictl get api-revisions -n PizzaShackAPI -v 1.0.0 -e dev 
                ```
                ```bash
                apictl get api-revisions --name PizzaShackAPI --version 1.0.0 --environment production
                ```    
                ```go
                apictl get api-revisions -n PizzaShackAPI -v 1.0.0 -q deployed:true -e dev 
                ```  

        -   **Response**

            ```go
            ID                                     REVISION            DESCRIPTION                                GATEWAY_ENVS
            8ee17243-e3c6-4517-b126-ec9745220004   1                  Initial Revision                           [Default Label3 Label4]
            660852cb-f23e-4d51-a622-0c4604f8598f   2                  Revision created after importing the API   [Label2]
            2812a8e8-c3b0-49c2-8023-435e27a888e4   3                  Revision created after importing the API   []
            f90fc252-5758-49ef-ab20-3d681f4b3238   4                  Revision created after importing the API   [Label1]
            4e4b87a8-209e-4193-9b7c-615678c04080   5                  Revision created after importing the API   []
            ```
            
    2. Get revisions for an API Product in an environment.

        -   **Command**
            ``` bash
            apictl get api-product-revisions -n <API-Product-name> -v <version> -e <environment> 
            ```
            ``` bash
            apictl get api-product-revisions --name <API-Product-name> --version <version> --environment <environment>
            ```
            ``` bash
            apictl get api-product-revisions --name <API-Product-name> --version <version> --provider <provider> --environment <environment> --query <deployment-search-query>
            ```

            !!! info
                **Flags:**  
                
                -   Required :  
                    `--name` or `-n` : Name of the API Product to get the revisions 
                    `--version` or `-v` : Version of the API Product to get the revisions    
                    `--environment` or `-e` : Environment to be searched  
                -   Optional :  
                    `--provider` or `-r` : Provider of the API Product
                    `--query` or `-q` : Search query pattern  
                    `--format` : pretty-print API Product revisions using Go templates

            !!! example
                ```bash
                apictl get api-product-revisions -n ShopProduct -v 1.0.0 -e dev 
                ```
                ```bash
                apictl get api-product-revisions --name MediaProduct --version 1.0.0 --environment production
                ```    
                ```go
                apictl get api-product-revisions -n PizzaProduct -v 1.0.0 -q deployed:true -e dev 
                ```  

        -   **Response**

            ```go
            ID                                     REVISION            DESCRIPTION         GATEWAY_ENVS
            86ae2e4f-59b4-45a8-8693-0edb64a7fd6a   1                   Initial Revision    [Default Label1]
            cbabfcca-7e53-4d9a-b07b-e5fc67768e0e   2                   Updated endpoints   [Label2 Label3]
            ```

            !!! tip 
                When using the `get api-revisions` and  `get api-product-revisions` command, `-q` or `--query` optional 
                flag can be used to filter out the revisions based on whether they are deployed in a gateway environment or not.
                ```--query deployed:true``` can be used to filter out the revisions that are already deployed in at least one
                gateway environment. Without the ```query``` flag, revisions will be displayed irrespective of the deployment.
            
            !!!note
                Output of the `get api-revisions` and `get api-product-revisions` commands can be formatted with Go Templates. For more information on formatting the get commands, see [Formatting the outputs of get commands]({{base_path}}/install-and-setup/setup/api-controller/advanced-topics/formatting-the-output-of-get-command).                

## Delete an API or API Product in an environment

Follow the instructions below to delete an API or Application in an environment using apictl:

1.  Make sure that the WSO2 API-M is started and the apictl is set up.   
For more information, see [Download and Initialize the apictl]({{base_path}}/install-and-setup/setup/api-controller/getting-started-with-wso2-api-controller/#download-and-initialize-the-apictl).
2.  Log in to the WSO2 API-M in the environment by following the instructions in [Login to an Environment]({{base_path}}/install-and-setup/setup/api-controller/getting-started-with-wso2-api-controller/#login-to-an-environment).
3.  Run the corresponding apictl command below to delete an API or an API Product in an environment.

    1. Delete an API in an environment.

        -   **Command**
            ``` bash
            apictl delete api -n <API name> -v <API version> -e <environment>
            ```
            ``` bash
            apictl delete api --name <API name> --version <API version> --environment <environment> 
            ```
            ``` bash
            apictl delete api --name <API name> --version <API version> --environment <environment> --provider <API provider> 
            ```

            !!! info
                **Flags:**  
                
                -   Required :  
                    `--environment` or `-e` : Environment from which the API should be deleted  
                    `--name` or `-n` : Name of the API to be deleted  
                    `--version` or `-v` : Version of the API to be deleted  
                -   Optional :  
                    `--provider` or `-r` : Provider of the API to be deleted  

            !!! example
                ```bash
                apictl delete api -n PizzaShackAPI -v 1.0.0 -e dev
                ```
                ```bash
                apictl delete api --name PizzaShackAPI --version 1.0.0 --environment production 
                ```    
                ```go
                apictl delete api --name PizzaShackAPI --version 1.0.0 --environment production --provider Alice 
                ```  

        -   **Response**

            ```go
            PizzaShackAPI API deleted successfully!
            ```

    2. Delete an API Product in an environment.

        -   **Command**
            ``` bash
            apictl delete api-product -n <API Product name> -v <API Product version> -e <environment> 
            ```
            ``` bash
            apictl delete api-product --name <API Product name> --version <API Product version> --environment <environment> 
            ```
            ``` bash
            apictl delete api-product --name <API Product name> --version <API Product version> --environment <environment> --provider <API Product provider> 
            ```

            !!! info
                **Flags:**  
                
                -   Required :  
                    `--environment` or `-e` : Environment from which the API Product should be deleted  
                    `--name` or `-n` : Name of the API Product to be deleted   
                    `--version` or `-v` : Version of the API Product to be deleted  
                -   Optional :  
                    `--provider` or `-r` : Provider of the API Product to be deleted  

            !!! example
                ```bash
                apictl delete api-product -n LeasingAPIProduct -v 1.0.0 -e dev 
                ```
                ```bash
                apictl delete api-product --name LeasingAPIProduct --version 1.0.0 -environment production 
                ```    
                ```go
                apictl delete api-product --name LeasingAPIProduct --version 1.0.0 --environment production --provider Alice 
                ```  

        -   **Response**

            ```go
            LeasingAPIProduct API Product deleted successfully!
            ```
    
## Change status of an API or API Product in an environment

Follow the instructions below to change the status of an API or API Product in an environment using apictl:

1.  Make sure that the WSO2 API-M is started and the apictl is set up.   
For more information, see [Download and Initialize the apictl]({{base_path}}/install-and-setup/setup/api-controller/getting-started-with-wso2-api-controller/#download-and-initialize-the-apictl).
2.  Log in to the WSO2 API-M in the environment by following the instructions in [Login to an Environment]({{base_path}}/install-and-setup/setup/api-controller/getting-started-with-wso2-api-controller/#login-to-an-environment).
3.  Run the corresponding apictl command below to change the status of an API or API Product in an environment.

    1. Change status of an API in an environment.

        -   **Command**
            ``` bash
            apictl change-status api -a <Action> -n <API name> -v <API version> -e <environment> 
            ```
            ``` bash
            apictl change-status api --action <Action> --name <API name> --version <API version> --environment <environment> 
            ```
            ``` bash
            apictl change-status api --action <Action> --name <API name> --version <API version> --environment <environment> --provider <API provider> 
            ```

            !!! info
                **Flags:**  
                
                -   Required :  
                    `--environment` or `-e` : The environment that the command is executed on  
                    `--name` or `-n` : The name of the respective API   
                    `--version` or `-v` : The version of the respective API   
                    `--action` or `-a` : The action to be taken to change the status of the API   
                -   Optional :  
                    `--provider` or `-r` : The provider of the respective API  

            !!! example
                ```bash
                apictl change-status api -a Publish -n PizzaShackAPI -v 1.0.0 -e dev 
                ```
                ```bash
                apictl change-status api --action "Publish" --name PizzaShackAPI --version 1.0.0 --environment production 
                ```    
                ```go
                apictl change-status api --action "Demote to Created" --name PizzaShackAPI --version 1.0.0 --environment production --provider Alice 
                ```  

        -   **Response**

            ```go
            PizzaShackAPI API state changed successfully!
            ```

    2. Change status of an API Product in an environment.

        -   **Command**
            ``` bash
            apictl change-status api-product -a <Action> -n <API Product name> -v <API Product version> -e <environment> 
            ```
            ``` bash
            apictl change-status api-product --action <Action> --name <API name> --version <API Product version> --environment <environment> 
            ```
            ``` bash
            apictl change-status api-product --action <Action> --name <API name> --version <API Product version> --environment <environment> --provider <API provider> 
            ```

            !!! info
                **Flags:**  
                
                -   Required :  
                    `--environment` or `-e` : The environment that the command is executed on  
                    `--name` or `-n` : The name of the respective API Product   
                    `--version` or `-v` : The version of the respective API Product   
                    `--action` or `-a` : The action to be taken to change the status of the API Product
                -   Optional :  
                    `--provider` or `-r` : The provider of the respective API Product 

            !!! example
                ```bash
                apictl change-status api-product -a Publish -n PizzaShackAPIProduct -v 1.0.0 -e dev 
                ```
                ```bash
                apictl change-status api-product --action "Publish" --name PizzaShackAPIProduct --version 1.0.0 --environment production 
                ```    
                ```go
                apictl change-status api-product --action "Demote to Created" --name PizzaShackAPIProduct --version 1.0.0 --environment production --provider Alice 
                ```  

        -   **Response**

            ```go
            API Product state changed successfully!
            ```

    !!! Info
        Supported action values : `Publish`, `Deploy as a Prototype`, `Demote to Created`, `Demote to Prototyped`, `Block`, `Deprecate`, `Re-Publish`, `Retire`.
        Note that the `Re-Publish` action is available only after calling Block action.

## Undeploy a revision of an API or API Product from all or specific deployment environments

Follow the instructions below to undeploy a revision of an API from a selected gateway environment using apictl:

1.  Make sure that the WSO2 API-M is started and the apictl is set up.   
For more information, see [Download and Initialize the apictl]({{base_path}}/install-and-setup/setup/api-controller/getting-started-with-wso2-api-controller/#download-and-initialize-the-apictl).
2.  Log in to the WSO2 API-M in the environment by following the instructions in [Login to an Environment]({{base_path}}/install-and-setup/setup/api-controller/getting-started-with-wso2-api-controller/#login-to-an-environment).
3.  Run the corresponding apictl command below to undeploy the revision from a gateway environment.

    1. Undeploy a revision of an API from gateway environments.
    
        -   **Command**
            ``` bash
            apictl undeploy api -n <API name> -v <API version> --rev <Revision number> -e <environment>
            ```
            ``` bash
            apictl undeploy api -n <API name> -v <API version> --rev <Revision number> -g <gateway environment> -e <environment> 
            ```
            ``` bash
            apictl undeploy api --name <API name> --version <API version> --rev <Revision number> --environment <environment> --provider <API provider> 
            ```
    
            !!! info
                **Flags:**  
                
                -   Required :  
                    `--environment` or `-e` : The environment that the command is executed on   
                    `--name` or `-n` : The name of the respective API  
                    `--version` or `-v` : The version of the respective API  
                    `--rev`  : Revision number of the respective API   
                -   Optional :  
                    `--provider` or `-r` : The provider of the respective API    
                    `--gateway-env` or `-g` : The gateway environment which the revisions needs to be undeployed  
    
            !!! example
                ```bash
                apictl undeploy api -n PizzaShackAPI -v 1.0.0 --rev 1 -e dev 
                ```
                ```bash
                apictl undeploy api -n PizzaShackAPI -v 1.0.0 --rev 2 -g Label1 -g Label2 -g Label3 -e production 
                ```    
                ```go
                apictl undeploy api --name PizzaShackAPI --version 1.0.0 --provider Alice --rev 3 --gateway-env Label1 --gateway-env Default --environment production 
                ```  
    
        -   **Response**
    
            ```go
            Revision 2 of API PizzaShackAPI_1.0.0 successfully undeployed from the specified gateway environments
            ```
            
    2. Undeploy a revision of an API product from gateway environments.
    
        -   **Command**
                ``` bash
                apictl undeploy api-product -n <API Product name> -v <API Product version> --rev <Revision number> -e <environment>
                ```
                ``` bash
                apictl undeploy api-product -n <API Product name> -v <API Product version> --rev <Revision number> -g <gateway environment> -e <environment> 
                ```
                ``` bash
                apictl undeploy api-product --name <API Product name> --version <API Product version> --rev <Revision number> --environment <environment> --provider <API Product provider>   
                ```
    
            !!! info
                **Flags:**  
                
                -   Required :  
                    `--environment` or `-e` : The environment that the command is executed on   
                    `--name` or `-n` : The name of the respective API Product    
                    `--version` or `-v` : The version of the respective API Product  
                    `--rev`  : Revision number of the respective API Product   
                -   Optional :  
                    `--provider` or `-r` : The provider of the respective API Product    
                    `--gateway-env` or `-g` : The gateway environment which the revisions needs to be undeployed    
           
            !!! example
                ```bash
                apictl undeploy api-product -n LeasingAPIProduct -v 1.0.0 --rev 1 -e dev 
                ```
                ```bash
                apictl undeploy api-product -n PizzaProduct -v 1.0.0  --rev 2 -g Label1 -g Label2 -g Label3 -e production 
                ```    
                ```go
                apictl undeploy api-product --name ShopProduct --version 1.0.0 --provider Alice --rev 3 --gateway-env Label1 --gateway-env Default  -environment production 
                ```  
         
            -   **Response**
        
                ```go
                Revision 2 of API Product PizzaProduct successfully undeployed from the specified gateway environments
                ```

    !!! Info
        - If ```--gateway-env``` or ```-g``` flag not provided, revision will be undeployed from all the gateway environments it is already deployed.
        - If there are multiple gateway environments, provide them one by one by specifying the flag ```--gateway-env``` or ```-g```. If a label has more than one words,
        wrap the entire label name with quotes.

## Get the log level of APIs or an API in an environment

Follow the instructions below to get the logging details of APIs or an API in an environment using apictl:

1.  Make sure that the WSO2 API-M is started and the apictl is set up.   
For more information, see [Download and Initialize the apictl]({{base_path}}/install-and-setup/setup/api-controller/getting-started-with-wso2-api-controller/#download-and-initialize-the-apictl).
2.  Log in to the WSO2 API-M in the environment by following the instructions in [Login to an Environment]({{base_path}}/install-and-setup/setup/api-controller/getting-started-with-wso2-api-controller/#login-to-an-environment).
3.  Run the corresponding apictl command below to get the logging details of APIs or an API in an environment.

    1. Get the logging details of APIs or an API in an environment.

        -   **Command**
            ``` bash
            apictl get api-logging -e <environment>
            ```
            ``` bash
            apictl get api-logging -e <environment> --tenant-domain <tenant domain> 
            ```
            ``` bash
            apictl get api-logging --environment <environment> --tenant-domain <tenant domain> 
            ```
            ``` bash
            apictl get api-logging  -e <environment> --api-id <api-id> 
            ```
            ``` bash
            apictl get api-logging  -e <environment> --api-id <api-id> --tenant-domain <tenant domain> 
            ```

            !!! info
                **Flags:**  
                
                -   Required :  
                    `--environment` or `-e` : The environment that the command is executed on  
                -   Optional :  
                    `--tenant-domain` : The tenant domain which you need to get the logging details of APIs or an API. If the flag is not provided, carbon.super will be used as the default value when executing the command    
                    `--api-id` : The UUID of the API which you need to get the logging details

            !!! example
                ```bash
                apictl get api-logging -e dev 
                ```
                ``` bash
                apictl get api-logging -e dev --tenant-domain wso2.com
                ```
                ``` bash
                apictl get api-logging --environment dev --tenant-domain wso2.com
                ```
                ``` bash
                apictl get api-logging  -e dev --api-id Bf36ca3a-0332-49ba-abce-e9992228ae06 
                ```
                ``` bash
                apictl get api-logging  -e dev --api-id Bf36ca3a-0332-49ba-abce-e9992228ae06 --tenant-domain wso2.com 
                ```   

        -   **Response**

            ```go
            API_ID 	                                     API_CONTEXT               	LOG_LEVEL
            Bf36ca3a-0332-49ba-abce-e9992228ae06         pizzashack/1.0.0	        FULL
            Af66fa7a-0546-49ba-adfe-a8976522ea96         sampleapi/1.1.0	        BASIC
            ```

    !!! Info
        - The `get api-logging` command can be executed only with a user who has super admin permissions.
        - Use the tenant-domain flag to get the logging details of the APIs in another tenant other than carbon.super tenant while you are logged in as a super admin user.

## Set the log level of an API in an environment

Follow the instructions below to add/change/remove the log level of an API in an environment using apictl:

1.  Make sure that the WSO2 API-M is started and the apictl is set up.   
For more information, see [Download and Initialize the apictl]({{base_path}}/install-and-setup/setup/api-controller/getting-started-with-wso2-api-controller/#download-and-initialize-the-apictl).
2.  Log in to the WSO2 API-M in the environment by following the instructions in [Login to an Environment]({{base_path}}/install-and-setup/setup/api-controller/getting-started-with-wso2-api-controller/#login-to-an-environment).
3.  Run the corresponding apictl command below to set the log level of an API in an environment.

    1. Set the log level of an API in an environment.

        -   **Command**
            ``` bash
            apictl set api-logging --api-id <api-id> --log-level <log level> --environment <environment>
            ```
            ``` bash
            apictl set api-logging --api-id <api-id> --log-level <log level> -e <environment>
            ```
            ``` bash
            apictl set api-logging --api-id <api-id> --log-level <log level> --environment <environment> --tenant-domain <tenant domain> 
            ```

            !!! info
                **Flags:**  
                
                -   Required :  
                    `--environment` or `-e` : The environment that the command is executed    
                    `--log-level`  : The log level of the API which you need to add/change/remove  
                    `--api-id`  : The UUID of the API which you need to add/change/remove the log level
                -   Optional :  
                    `--tenant-domain` : The tenant domain which you need to add/change/remove the log level of an API. If the flag is not provided, carbon.super will be used as the default value when executing the command

            !!! example
                ``` bash
                apictl set api-logging --api-id Bf36ca3a-0332-49ba-abce-e9992228ae06 --log-level full --environment dev
                ```
                ``` bash
                apictl set api-logging --api-id Bf36ca3a-0332-49ba-abce-e9992228ae06 --log-level full -e dev
                ```
                ``` bash
                apictl set api-logging --api-id Bf36ca3a-0332-49ba-abce-e9992228ae06 --log-level full --environment dev --tenant-domain wso2.com 
                ```   

        -   **Response**

            ```go
            Log level FULL is successfully set to the API.
            ```

    !!! Info
        - Supported log-level values : `FULL`, `BASIC`, `STANDARD`, `OFF`.
        - When you need to disable logging for an API, set the log level to OFF.
