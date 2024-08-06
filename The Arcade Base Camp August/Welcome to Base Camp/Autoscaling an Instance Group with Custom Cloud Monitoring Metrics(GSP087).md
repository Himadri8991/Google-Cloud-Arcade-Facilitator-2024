# Autoscaling an Instance Group with Custom Cloud Monitoring Metrics || [GSP087](https://www.cloudskillsboost.google/games/5383/labs/34947) ||

### Run the following Commands in CloudShell

```
export ZONE=
```


```
gsutil mb gs://$DEVSHELL_PROJECT_ID

gsutil cp -r gs://spls/gsp087/* gs://$DEVSHELL_PROJECT_ID


Task 2 Completed

gcloud compute instance-templates create autoscaling-instance01 --metadata=startup-script-url=gs://$DEVSHELL_PROJECT_ID/startup.sh,gcs-bucket=gs://$DEVSHELL_PROJECT_ID

Task 3 Completed

gcloud beta compute instance-groups managed create autoscaling-instance-group-1 --project=$DEVSHELL_PROJECT_ID --base-instance-name=autoscaling-instance-group-1 --size=1 --template=projects/$DEVSHELL_PROJECT_ID/global/instanceTemplates/autoscaling-instance01 --zone=$ZONE --list-managed-instances-results=PAGELESS --no-force-update-on-repair --default-action-on-vm-failure=repair && gcloud beta compute instance-groups managed set-autoscaling autoscaling-instance-group-1 --project=$DEVSHELL_PROJECT_ID --zone=$ZONE --cool-down-period=60  --max-num-replicas=3 --min-num-replicas=1 --mode=on --target-cpu-utilization=0.6 --stackdriver-metric-filter=resource.type\ =\ \"gce_instance\" --update-stackdriver-metric=custom.googleapis.com/appdemo_queue_depth_01 --stackdriver-metric-utilization-target=150.0 --stackdriver-metric-utilization-target-type=gauge


Task 4 & 7  Completed

Lab Completed !!!

echo "${CYAN}${BOLD}With Regards Himadri${RESET}"
#-----------------------------------------------------end----------------------------------------------------------#

```

# Congratulations 🎉 for completing the Lab !

##### *You Have Successfully Demonstrated Your Skills And Determination.*

#### *Well done!*

#### Don't Forget to Join the [WhatsApp Group](https://chat.whatsapp.com/CcX9gXycV1lKmOjnZQCk7g) 
