# SecTrainingData
Data for training machine learning models related to bug bounty and pentesting.
## Images Data
- Images of webpages organized by prediction tagging
- Images of VNC and RDP services (These will likely be two categories, normal ones with an expected login prompt and ones with no login or default username added)
## Text Data
Nothing there at this time, but I have to have data for the following scenarios.
- Payloads for training attacks (SQLi, XSS, XXE, SSRF, Content brute forcing, Etc.)
- Tool output logs for anomaly detection

# Images Usage Guide
### 1. Create project at https://www.customvision.ai
### 2. Upload Images using foldername as tag
### 3. Train your model
### 4. Once your model is trained you are all set to start sending images to your API.

> Note: I'm currently working on a tool that will work with screenshotting tools to check against the API. For now the following bash script works ok.
``` 
IMAGES=$(ls | grep ".*\.png$")
URL="{Prediction URL}"
KEY="{Prediction Key"
for image in $IMAGES
do
  echo "Checking: $image"
  cat $image | curl -s -X POST "$URL" \
  -H "Prediction-Key: $KEY" \
  -H "Content-Type: application/octet-stream" \
  --data-binary "@-" | jq '.predictions[0] | {tagName,probability} '
done
```
### 5. After you have done some predictions. You can go back to the portal and add tags to ones you recently sent to the API make your predictions better.
