# Step 3: Upgrade Runtime & Frameworks

## 🎯 Goal

Upgrade the application from Java 8 to Java 21 and from Spring Boot 2.x to 3.x using GitHub Copilot app modernization's automated upgrade tasks.

## Run the Java Upgrade Task

1. In the **Java Upgrade** table at the bottom of the **Issues** tab, click the **Run Task** button of the first entry **Java Version Upgrade**.

    ![Java Upgrade](../doc-media/java-upgrade.png)

1. After clicking the **Run Task** button, the Copilot Chat panel will open with Agent Mode. The agent will check out a new branch and start upgrading the JDK version and Spring/Spring Boot framework. Click **Allow** for any requests from the agent.

## What the Upgrade Does

The automated upgrade will:
- Update the Java version in `pom.xml` from 8 to 21
- Upgrade Spring Boot dependencies from 2.x to 3.x
- Update incompatible APIs (e.g., `javax.*` → `jakarta.*` namespace changes)
- Fix deprecated method calls and patterns
- Update Maven plugin versions as needed

> [!NOTE]
> The upgrading tool also supports upgrading to JDK 25 (the latest LTS version). To do this, click on the generated chat message, edit the target Java version to 25, and then click **Send** to apply the change.

## Review the Changes

After the agent completes its work:
1. Review the changes in the diff view
2. Verify that `pom.xml` reflects the new Java and Spring Boot versions
3. Check that namespace changes (`javax` → `jakarta`) have been applied
4. Click **Keep** to apply the changes

## ✅ Checkpoint

- [ ] Java Version Upgrade task executed
- [ ] Agent completed the upgrade process
- [ ] Changes reviewed in diff view
- [ ] Java version updated to 21 in `pom.xml`
- [ ] Spring Boot upgraded to 3.x

👉 **[Continue to Step 4: Health Endpoints →](04-health-endpoints.md)**
