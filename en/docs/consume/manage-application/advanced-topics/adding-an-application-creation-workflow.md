# Adding an Application Creation Workflow

Attaching a custom workflow to application creation provides the ability to control the creation of applications (approve or reject the request for application creation) in the Developer Portal. An application is an entity that holds a set of subscribed APIs, accessed by an authorization key generated for that particular application. Therefore, controlling the creation of these applications would be a decision based on the organization's requirements. 

Example usecase:

-   Review the information that corresponds to an application by a specific reviewer before the application is created.
-   The application creation would be offered as a paid service.
-   The application creation should be allowed only to users who are in a specific role.


## Engage the Approval Workflow Executor in API Manager

1. Sign in to WSO2 API-M Admin Portal (`https://<Server-Host>:9443/admin`).

2. Navigate to **Settings** --> **Advanced** section.
    
3. Add the following under **Workflows** configuration section and enable **Approval Workflow Executor** for application creation.

    ``` json
    "Workflows" : {
        ...
        "ApplicationCreation" : {},
        ...
    }
    ```

    Once the changes are done, click on `Save` and save the new configuration . The approval workflow is now engaged.

4.  Create an application via the Developer Portal.
    
    1. Sign in to the Developer Portal.

         (`https://localhost:9443/devportal`)

    2. Click **Applications** --> **ADD NEW APPLICATION** and create a new application.
                  
         Note that the **Status** field of the application states **INACTIVE** (Waiting for approval)

    ![Application status is INACTIVE - Waiting for approval]({{base_path}}/assets/img/learn/application-creation-inactive.png)

5.  Sign in to the Admin Portal (`https://localhost:9443/admin`), list all the tasks for application creation  from **Tasks** --> **Application Creation** and approve or reject the task. 
     
    ![Approve tasks]({{base_path}}/assets/img/learn/application-creation-pending-request.png)

6.  Go back to the **Applications** page in the WSO2 Developer Portal and see the created application.

    Check whether the status is updated to **ACTIVE** or **REJECTED**.