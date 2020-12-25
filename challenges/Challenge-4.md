# Implement continuous deployment (CD)

**Resist the initial temptation to rush on the keyboard! This is the time to pause and think as a team about your end-to-end deployment process that you would implement in this company.**

**Reminders:**

- Use an InPrivate/Incognito window in your browser to avoid any confusion with any other credentials that you may use to access Azure resources.

--------------

Now that you have successfully implemented continuous integration, it is time to show that you can deploy the container images that you have built for each of the four APIs to Azure App Service.

The code and tests for the APIs is available in the following GitHub repository:

- <a href="https://github.com/Azure-Samples/openhack-devops-team" target="_blank">Azure-Samples/openhack-devops-team</a>

Before you joined the event, **each** API of the MyDriving application was built and deployed to an existing Azure Container Registry using the following scripts:

- POI API deployment script

    ```sh
    echo "Building API-POI image..."
    echo "Changing directory to $GITOHTEAMDIRPATH/apis/poi/web..."
    cd "$GITOHTEAMDIRPATH/apis/poi/web"
    az acr build --image "devopsoh/api-poi:${BASEIMAGETAG}" --registry $ACRNAME --file Dockerfile .
    ```

- Trips API deployment script

    ```sh
    echo "Building API-TRIPS image..."
    echo "Changing directory to $GITOHTEAMDIRPATH/apis/trips..."
    cd "$GITOHTEAMDIRPATH/apis/trips"
    az acr build --image "devopsoh/api-trips:${BASEIMAGETAG}" --registry $ACRNAME --file Dockerfile .
    ```

- User API deployment script

    ```sh
    echo "Building API-USERPROFILE image..."
    echo "Changing directory to $GITOHTEAMDIRPATH/apis/userprofile..."
    cd "$GITOHTEAMDIRPATH/apis/userprofile"
    az acr build --image "devopsoh/api-userprofile:${BASEIMAGETAG}" --registry $ACRNAME --file Dockerfile .
    ```

- User-Java API deployment script

    ```sh
    echo "Building API-USER-JAVA image..."
    echo "Changing directory to $GITOHTEAMDIRPATH/apis/user-java..."
    cd "$GITOHTEAMDIRPATH/apis/user-java"
    az acr build --image "devopsoh/api-user-java:${BASEIMAGETAG}" --registry $ACRNAME --file Dockerfile .
    ```

## Challenge

Using the tooling that you have implemented so far, you must deploy each of the four APIs to your existing Azure App Service using <a href="https://continuousdelivery.com/" target="_blank">Continuous Delivery</a> (CD), but before you are able to deploy you will need to push the images to a container registry. Configuration steps will differ depending on whether your team decides to use Azure Container Registry or GitHub Packages to store your images.

**Reminders:**

- The image tag should take the format of:
    - If using Azure Container Registry
        - `<Azure Container Registry URI>/<ACR_repository_name>:<Revision Number>` where the `ACR_repository_name` follows the naming convention `devopsoh/<image_name>:<tag>`.
    - If using GitHub Packages
        - `docker.pkg.github.com/<Owner>/<Repository name>/<Image Name>:<Revision Number>` where image name should be the images you are building (eg: `api-trips`)
        - Tip: GitHub Actions provides you with a set of <a href="https://help.github.com/actions/configuring-and-managing-workflows/using-environment-variables#default-environment-variables" target="_blank">predefined variables</a> that can help you

- The following tools have been tested with this challenge. You may use any other set of tools however the coaches will only be able to provide limited guidance:

    - Orchestrators
        - **<a href="https://github.com/features/actions" target="_blank">GitHub Actions</a>**
        - **<a href="https://azure.microsoft.com/services/devops/pipelines/" target="_blank"> Azure  Pipelines</a>** Part of Azure DevOps, formerly known as Visual Studio Team Services (VSTS)</a>
        - **<a href="https://jenkins.io/" target="_blank">Jenkins</a>**
    - Version Control
        - **<a href="https://github.com/" target="_blank">GitHub</a>**
    - Docker Registry
        - **<a href="https://azure.microsoft.com/services/container-registry/" target="_blank">Azure Container Registry</a>**
        - **<a href="https://github.com/features/packages" target="_blank">GitHub Packages</a>**

## Success Criteria

Your coach will provide you with an update to your APIs. You must demonstrate that you can reference the deployment of these API updates with the corresponding work items.

Demonstrate to your coach that in your build/workflow:

- The container images (one per API) are published to the registry of your choice (only when building `master` but not on PRs).

    > **Note:** Your publish process should not overwrite the existing image with the *latest* tag, so consider how you will insure unique values for image tags.

- The API(s) code is deployed to the Azure App Service every time code is pushed to master (if the code compiles and all tests pass, but only when building `master` branch).

    > **Note:** Your branch/pull request policy can be used to enforce workflow and gates between CI and CD activities.

## References

- Continuous Delivery
    - <a href="https://docs.microsoft.com/azure/devops/learn/what-is-continuous-delivery" target="_blank">What is Continuous Delivery?
    </a>
    - <a href="https://continuousdelivery.com/#why-continuous-delivery" target="_blank">Why continuous delivery?</a>
- Github
    - <a href="https://github.com/docker/build-push-action" target="_blank">GitHub Actions - Docker build and push</a>
    - <a href="https://github.com/marketplace/actions/azure-webapp" target="_blank">GitHub Actions - Azure WebApp</a>
- Azure Pipelines
    - <a href="https://docs.microsoft.com/azure/app-service/containers/quickstart-docker" target="_blank">Azure Pipelines - Deploy a custom Linux container to Azure App Service</a>
    - <a href="https://docs.microsoft.com/azure/app-service/containers/tutorial-custom-docker-image" target="_blank">Azure Pipelines - Tutorial: Build a custom image and run in App Service from a private registry</a>
    - <a href="https://docs.microsoft.com/azure/devops/pipelines/tasks/build/docker?view=azure-devops" target="_blank">Azure Pipelines - Docker task</a>
- Docker Registries
    - <a href="https://help.github.com/packages" target="_blank">GitHub Packages Documentation</a>
    - <a href="https://docs.microsoft.com/azure/container-registry/" target="_blank">Azure Container Registry documentation</a>
