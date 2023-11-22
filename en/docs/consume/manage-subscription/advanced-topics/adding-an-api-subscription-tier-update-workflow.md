# Adding an API Subscription Tier Update Workflow

[Subscription Tier update]({{base_path}}/consume/manage-subscription/subscribe-to-an-api/) will provide the capability to change the subscription tier of an already existing subscription. Attaching a custom workflow to the API subscription update, enables an admin to approve/reject the subscription tier change request made for an active subscription. Note that only an admin is able to approve/reject a subscription tier change request.

When the API subscription update workflow is enabled, when the subscription tier change request is made, the subscription status is changed to the `TIER_UPDATE_PENDING` state. In this state, a consumer can still invoke the API with the same subscription (with the previous existing subscription tier), using its production or sandbox keys, until the subscription update to a new tier is approved. Once the subscription status change request is approved the subscription status is updated to the `UNBLOCKED` state.

#### Engaging the Approval Workflow Executor in the API Manager

1. Sign in to WSO2 API-M Admin Portal (`https://<Server-Host>:9443/admin`).

2. Navigate to **Settings** --> **Advanced** section.
    
3. Add the following under **Workflows** configuration section and enable **Approval Workflow Executor** for subscription update.

    ``` json
    "Workflows" : {
        ...
        "SubscriptionUpdate" : {},
        ...
    }
    ```

    Once the changes are done, click on `Save` and save the new configuration . The approval workflow is now engaged.

4.  Sign in to the WSO2 API Developer Portal (`https://<hostname>:<port>/devportal`) and click **Applications**. Select the application which has the subscriptions you wish to modify.

    [![Applications Overview Tab]({{base_path}}/assets/img/learn/application-overview.png)]({{base_path}}/assets/img/learn/application-overview.png)


5. Click **Subscriptions** to list the subscriptions of the application.
    
    [![Subscriptions Overview Tab]({{base_path}}/assets/img/learn/subscriptions-overview-tab.png)]({{base_path}}/assets/img/learn/subscriptions-overview-tab.png)

     
6.  Select the subscription which the tier needs to be changed and click the **EDIT** icon to open the **Subscription Update** popup.

    [![Subscription Update Popup]({{base_path}}/assets/img/learn/subscription-update-popup-start.png)]({{base_path}}/assets/img/learn/subscription-update-popup-start.png)

7.  Select the throttling tier that needs to be updated and click **Update** to continue. After updating you will see the subscription status as **TIER_UPDATE_PENDING**.

    [![Subscription Update Before Approval]({{base_path}}/assets/img/learn/subscription-update-before-approval.png)]({{base_path}}/assets/img/learn/subscription-update-before-approval.png)
    
8.  (Optional) if the consumer need to update the requested tier to a different tier, click **EDIT** icon and select the new requested tier and click **Update**.
    
    [![Subscription Update New Tier Request]({{base_path}}/assets/img/learn/subscription-update-new-tier-request.png)]({{base_path}}/assets/img/learn/subscription-update-new-tier-request.png)
    
9.  Sign in to the Admin Portal (`https://<Server Host>:9443/admin`), list all the tasks for API subscription update from **Tasks** --> **Subscription Update** and click on approve (or reject) to approve (or reject) the workflow pending request.

    [![Subscription Update Admin]({{base_path}}/assets/img/learn/subscription-update-admin-entry.png)]({{base_path}}/assets/img/learn/subscription-update-admin-entry.png)

10.  After approving go back to the API Developer Portal Application Subscriptions tab, the subscription status will be **UNBLOCKED** and, the requested tier will also be assigned.
     
    [![Subscription Update completed]({{base_path}}/assets/img/learn/subscription-update-completed.png)]({{base_path}}/assets/img/learn/subscription-update-completed.png)

    Now the consumer can use the existing subscription with the newly assigned throttling tier.

    
