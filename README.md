# Objective :# Objective :

Setup up an infrastructure such as there are three teams/environemnts :

1. Production
2. Testing
3. Quality Assurance

Production Team will deploy the code first, now there is some work going on in the developement team which is to be deployed on testing environment which will be sent to the production only when the QA team approves it.

## Requirements :

1. Docker
   - Image: httpd
2. Jenkins
   - Github Plugin
3. System with 2gb ram (Recommended)
4. Git and Hooks
5. Github and Github Webhooks
6. ngrok

# My Approach

1. Made 3 Jobs for produnction, testing and Quality Assurance

2. Make Environments for production and testing. I am using docker here, I have created a volume(persistant storage) for production and testing and mounted them to their respective containers

## Process :

### Operations Side:

1. My job 1 and job2 will get their code from the github (from their respective branches => master:production, dev:testing)
2. Both the containers have diferent web addresses so the quality team can monitor both
3. Quality team continously checks for changes in testing environemnt, and decides wether to approves it or not
4. On approval QA team manually builds the job3
5. Since job three is the upstream job of job2 and job1 , so on succesfull approval foloowong things will happen:
   1. Dev and Master branch will be merged
   2. Code will be pushed to the github
   3. job 1 and job2 will be build

- ngrok will be running in the system to provide public accessable addres so that github webhook will work and production site can be accessible to the public

### Developer site :

1. Created a hook for post-commit and post-merge so the developer need not to be manually push the code each time he commits

   ![edit](https://raw.githubusercontent.com/devmohit-live/Images_of_repo/master/localhook.JPG)

   ![](https://raw.githubusercontent.com/devmohit-live/Images_of_repo/master/mergeproof.JPG)

2. Added The webhooks to the Jenkins Github API :=> ip/github-webhook/

   ![Producntion](https://raw.githubusercontent.com/devmohit-live/Images_of_repo/master/webhooks.JPG)

## Screenshots :

## 1. Initially:

1. Production:
   ![Producntion](https://raw.githubusercontent.com/devmohit-live/Images_of_repo/master/pro01.JPG)
2. Testing :
   ![Testing](https://raw.githubusercontent.com/devmohit-live/Images_of_repo/master/test01.JPG)

## 2. Changed made but not approved:

1. Produnction:
   ![Producntion](https://raw.githubusercontent.com/devmohit-live/Images_of_repo/master/pro01.JPG)
2. Testing :
   ![Testing](https://raw.githubusercontent.com/devmohit-live/Images_of_repo/master/test02.JPG)
3. QA Rejected

## Changed and approved:

1. Testing :
   ![Testing](https://raw.githubusercontent.com/devmohit-live/Images_of_repo/master/test03.JPG)
2. QA Approved:
   ![QA0](https://raw.githubusercontent.com/devmohit-live/Images_of_repo/master/qa0.JPG)
   ![QA1](https://raw.githubusercontent.com/devmohit-live/Images_of_repo/master/qa1.JPG)
   ![QA2](https://raw.githubusercontent.com/devmohit-live/Images_of_repo/master/qa2_log.JPG)

3. Production:
   ![Producntion](https://raw.githubusercontent.com/devmohit-live/Images_of_repo/master/finalprod.JPG)

## Steps and Configurations Screenshots :

## 1. Production:

    1. Created a job for cloning the Github repo's master branch which is to be deployed on docker.
    Github Githook trigger is checked so that whenever the developer pushes the code, github webhook will be activated and it will contact jenkins, then jenkins will pull the updated code, and move it to the created volume.

![01](https://raw.githubusercontent.com/devmohit-live/Images_of_repo/master/1a01.JPG)

    2. Provided the command to check wether the docker conatiner is already running, if not create it mount the volume and expose it's port 80 to base os port 8082.

![02](https://raw.githubusercontent.com/devmohit-live/Images_of_repo/master/1a02.JPG)

## 2. Testing:

    1. Created a job for cloning the Github repo's master branch which is to be deployed on docker.
    Github Githook trigger is checked so that whenever the developer pushes the code, github webhook will be activated and it will contact jenkins, then jenkins will pull the updated code, and move it to the created volume.

![01](https://raw.githubusercontent.com/devmohit-live/Images_of_repo/master/1b.JPG)

    2. Provided the command to check wether the docker conatiner is already running, if not create it mount the volume and expose it's port 80 to base os port 8083
    QA team will check the testing environment at this port address.

![02](https://raw.githubusercontent.com/devmohit-live/Images_of_repo/master/1b02.JPG)

## 2. QA Team :

    1. Provided the github repo link along with credentials as on approval there should be a merge between the master and dev branch, and also the code should be pushed to github.

![01](https://raw.githubusercontent.com/devmohit-live/Images_of_repo/master/1c00.JPG)

    2. Details is provided to the additional behaviour so that merging could be done.

![02](https://raw.githubusercontent.com/devmohit-live/Images_of_repo/master/1c01.JPG)

    3. Post Build Action deatils provided, so that push after the merge can be done

![02](https://raw.githubusercontent.com/devmohit-live/Images_of_repo/master/1c03.JPG)

    4. After the push is being done. This job will call the job1 and job2 so that the code can be updated. (This part can be omitted as webhook will do it's job, but to be on safe side, I have put these projects as downstream projects)

![02](https://raw.githubusercontent.com/devmohit-live/Images_of_repo/master/1c04.JPG)
