# Autoscaling an Instance Group with Custom Cloud Monitoring Metrics || [GSP087](https://www.cloudskillsboost.google/games/5383/labs/34947) ||

### Run the following Commands in CloudShell

```
export ZONE=
```
### From "Task 4" you can find your REGION,

```
BLACK=`tput setaf 0`
RED=`tput setaf 1`
GREEN=`tput setaf 2`
YELLOW=`tput setaf 3`
BLUE=`tput setaf 4`
MAGENTA=`tput setaf 5`
CYAN=`tput setaf 6`
WHITE=`tput setaf 7`

BG_BLACK=`tput setab 0`
BG_RED=`tput setab 1`
BG_GREEN=`tput setab 2`
BG_YELLOW=`tput setab 3`
BG_BLUE=`tput setab 4`
BG_MAGENTA=`tput setab 5`
BG_CYAN=`tput setab 6`
BG_WHITE=`tput setab 7`

BOLD=`tput bold`
RESET=`tput sgr0`
#----------------------------------------------------start--------------------------------------------------#

echo "${YELLOW}${BOLD}

Starting Execution 


${RESET}"
#gcloud auth list
#gcloud config list project
export PROJECT_ID=$(gcloud info --format='value(config.project)')
#export BUCKET_NAME=$(gcloud info --format='value(config.project)')
#export EMAIL=$(gcloud config get-value core/account)
#gcloud config set compute/region $region
#gcloud config set compute/zone $region-a
#export ZONE=$region-a



#USER_EMAIL=$(gcloud auth list --limit=1 2>/dev/null | grep '@' | awk '{print $2}')
#----------------------------------------------------code--------------------------------------------------# 

gsutil mb gs://$DEVSHELL_PROJECT_ID

gsutil cp -r gs://spls/gsp087/* gs://$DEVSHELL_PROJECT_ID

echo "${GREEN}${BOLD}Task 2 Completed${RESET}"

gcloud compute instance-templates create autoscaling-instance01 --metadata=startup-script-url=gs://$DEVSHELL_PROJECT_ID/startup.sh,gcs-bucket=gs://$DEVSHELL_PROJECT_ID


echo "${GREEN}${BOLD}Task 3 Completed${RESET}"

gcloud beta compute instance-groups managed create autoscaling-instance-group-1 --project=$DEVSHELL_PROJECT_ID --base-instance-name=autoscaling-instance-group-1 --size=1 --template=projects/$DEVSHELL_PROJECT_ID/global/instanceTemplates/autoscaling-instance01 --zone=$ZONE --list-managed-instances-results=PAGELESS --no-force-update-on-repair --default-action-on-vm-failure=repair && gcloud beta compute instance-groups managed set-autoscaling autoscaling-instance-group-1 --project=$DEVSHELL_PROJECT_ID --zone=$ZONE --cool-down-period=60  --max-num-replicas=3 --min-num-replicas=1 --mode=on --target-cpu-utilization=0.6 --stackdriver-metric-filter=resource.type\ =\ \"gce_instance\" --update-stackdriver-metric=custom.googleapis.com/appdemo_queue_depth_01 --stackdriver-metric-utilization-target=150.0 --stackdriver-metric-utilization-target-type=gauge

echo "${GREEN}${BOLD}Task 4 & 7  Completed${RESET}"
echo "${GREEN}${BOLD}Lab Completed !!!${RESET}"

echo "${CYAN}${BOLD}With Regards Himadri${RESET}"
#-----------------------------------------------------end----------------------------------------------------------#

```

# Congratulations 🎉 for completing the Lab !

##### *You Have Successfully Demonstrated Your Skills And Determination.*

#### *Well done!*

#### Don't Forget to Join the [WhatsApp Group](https://chat.whatsapp.com/CcX9gXycV1lKmOjnZQCk7g) 
