# Step 4: Expose Health Endpoints using Custom Tasks

## 🎯 Goal

Use custom tasks to expose health endpoints for your applications using Spring Boot Actuator, without writing code yourself.

> [!NOTE]
> Custom tasks are not supported for the IntelliJ IDEA plugin. If you are using IntelliJ IDEA, you can skip this section.

## Create a Custom Task

1. Open the sidebar of `GITHUB COPILOT APP MODERNIZATION`. Click the `+` button in the **Tasks** view to create a custom task.

   ![Create Formula From Source Control](../doc-media/create-formula-from-source-control.png)

1. In the opened tab, enter the **Task Name** and **Task Prompt** as shown below:
   - **Task Name**: Expose health endpoint via Spring Boot Actuator
   - **Task Prompt**: You are a Spring Boot developer assistant, follow the Spring Boot Actuator documentation to add basic health endpoints for Azure Container Apps deployment.

1. Click the **Add References** button to add the Spring Boot Actuator official documentation as references.

   ![Health endpoint task](../doc-media/health-endpoint-task.png)

1. In the popped-up quick-pick window, select **External links**. Then paste the following link: `https://docs.spring.io/spring-boot/reference/actuator/endpoints.html`. Click **Save** to create the task.

## Run the Custom Task

1. Click the **Run** button to trigger the custom task.
1. Follow the same steps as the predefined task to review and apply the changes.
1. Review the proposed code changes and click **Keep** to apply them.

## What This Does

The custom task will:
- Add the Spring Boot Actuator dependency to `pom.xml`
- Configure health endpoints in `application.properties` or `application.yml`
- Expose `/actuator/health` endpoint for Azure Container Apps health probes
- This is essential for cloud deployment where the platform needs to check if your app is healthy

> [!TIP]
> Custom tasks are a powerful feature of GitHub Copilot app modernization. You can create tasks for any modernization need by providing a descriptive prompt and relevant documentation references.

## ✅ Checkpoint

- [ ] Custom task created with the correct name and prompt
- [ ] Spring Boot Actuator documentation added as reference
- [ ] Task executed successfully
- [ ] Health endpoint code changes reviewed and applied
- [ ] `/actuator/health` endpoint will be available when the app runs

👉 **[Continue to Step 5: Containerize Applications →](05-containerize.md)**
