Once you make changes in VS Code, this is your update flow:

1. Edit Code

Example:

chat_service.py
index.html
main.py

Save the files.

2. Build New Docker Image

Increment version:

docker build -t servicenow-agent:v4 .
3. Tag for ACR
docker tag servicenow-agent:v4 satopsagent2026.azurecr.io/servicenow-agent:v4
4. Push to Azure Container Registry
docker push satopsagent2026.azurecr.io/servicenow-agent:v4

Wait until push completes.

5. Update Container App
az containerapp update --name sat-servicenow-agent --resource-group sat-rg-servicenow-agent --image satopsagent2026.azurecr.io/servicenow-agent:v4
6. Verify Deployment
az containerapp revision list --name sat-servicenow-agent --resource-group sat-rg-servicenow-agent -o table

You should see a new revision.

7. Refresh Website

Open: https://sat-servicenow-agent.wittypebble-1e3cb50a.centralindia.azurecontainerapps.io
