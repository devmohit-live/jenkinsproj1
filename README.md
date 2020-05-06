# Objective : Setup up an infrastructure such as there are three teams/environemnts :

1. Production
2. Testing
3. Quality Assurance

Production Team will will deploy the code first, now there is some work going on in the developement team which is to be deployed on testing environment which will be sent to the production only when the QA team approves it.

# My Approach

1. Made 3 Jobs for produnction, testing and QA
2. Make Environments for production and testing => I am using docker here, I have created a volume(persistant storage) for production and testing and mounted them to their respective containers

## Steps

1. My job 1 and job2 will get their code from the github (from their respective branches => master:production, dev:testing)
2. Both the containers have diferent web addresses so the quality team can monitor both
3. Quality team continously checks for changes in testing environemnt, and decides wether to approves it or not
4. On approval QA team manually builds the job3
5. Since job three is the upstream job of job2 and job1 , so on succesfull approval foloowong things will happen:
   1. Dev and Master branch will be merged
   2. Code will be pushed to the github
   3. job 1 and job2 will be build

## Here are some Images:

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

## Configurations:

## 1. Production:

![01](https://raw.githubusercontent.com/devmohit-live/Images_of_repo/master/1a01.JPG)

![02](https://raw.githubusercontent.com/devmohit-live/Images_of_repo/master/1a02.JPG)

## 2. Testing:

![01](https://raw.githubusercontent.com/devmohit-live/Images_of_repo/master/1b.JPG)

![02](https://raw.githubusercontent.com/devmohit-live/Images_of_repo/master/1b02.JPG)

## 2. QA Team :

![01](https://raw.githubusercontent.com/devmohit-live/Images_of_repo/master/1c00.JPG)

![02](https://raw.githubusercontent.com/devmohit-live/Images_of_repo/master/1c01.JPG)

![02](https://raw.githubusercontent.com/devmohit-live/Images_of_repo/master/1c03.JPG)

![02](https://raw.githubusercontent.com/devmohit-live/Images_of_repo/master/1c04.JPG)
