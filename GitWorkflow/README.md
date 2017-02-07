# Git Workflow

## Table of Contents

1. [Clone Onelogin Repository](#clone-onelogin-repository)
2. [Git-flow Terminology](#git-flow-terminology)
3. [Visualize Gitflow](#visualize-gitflow)
4. [Start New Release](#start-new-release)
5. [Start New Feature](#start-new-feature)
6. [Start New Feature out of existing one](#start-new-feature-out-of-existing-one)
7. [Start New Hotfix](#start-new-hotfix)
8. [Commit Messages](#commit-messages)
9. [Create Pull Request](#create-pull-request)
10. [Code Review Checklist](#code-review-checklist)
11. [Naming Conventions](#naming-conventions)


## Clone Onelogin Repository
1. Clone the repository in your desired directory
`git clone https://github.com/vodafone-germany/onelogin`
2. Cd to the cloned directory
`cd onelogin`
3. Install Dependencies
`npm install`
4. Run `ng serve`
5. Open `localhost:4200` in the browser

## Git-flow Terminology
**Branch:** Group of different features, Features or ideas.

**Master Branch:** Is the base for all branches and the branch which contains the stable code on the production environment. 

**Develop Branch:** All code ready for production on a staging environment.

**Feature:** Active code that is already in development. Usually related to a ticket/story.

**Release:** Integration branch to test develop testing into master.

**Hotfix Branch:** Emergency fix for production site.
## Visualize Gitflow
![visualize git](https://cloud.githubusercontent.com/assets/12252068/22692749/14d09ea8-ed49-11e6-9c68-9fc5435613a4.png)
## Start New Release
1. Switch to sprint branch
2. Click on Git flow                                                       
![gitflow](https://cloud.githubusercontent.com/assets/12252068/22692868/8e6e030e-ed49-11e6-8fb5-c424f54df136.png)

3. Click on **Start New Release**.                                          
![new release](https://cloud.githubusercontent.com/assets/12252068/22692912/c1cd5128-ed49-11e6-8a6e-12d6ee8fd95a.png)

4. Type the Name of the release as follows and choose the **Latest development branch** Option.                             
![git new](https://cloud.githubusercontent.com/assets/12252068/22692977/0880d0e0-ed4a-11e6-9358-13d253ab5001.png)

5. The release will be successfully created below release folder.

## Start New Feature
1. Switch to sprint branch.
2. Click on Git flow.                       
![gitflow](https://cloud.githubusercontent.com/assets/12252068/22692868/8e6e030e-ed49-11e6-8fb5-c424f54df136.png)

3.	The following screen will appear click on **Other Actions**,Then click on **Start New Feature**.               
![new fe](https://cloud.githubusercontent.com/assets/12252068/22693084/864756b6-ed4a-11e6-8e1a-c873e1f380b1.jpg)

4. Type Feature Name in the appeared window following this format “Feature_Name”, Select **Latest development branch** Option and click Ok.                    
![fe _name](https://cloud.githubusercontent.com/assets/12252068/22693170/c8f1fee4-ed4a-11e6-92ab-7f0101fc1f69.png)

5.	The feature is created below “feature” folder and you are switched automatically to the created feature successfully.
![view_fe](https://cloud.githubusercontent.com/assets/12252068/22693198/e8943f64-ed4a-11e6-9bbb-01a30251c175.png)

## Start New Feature out of existing one
1.	Make Sure that you are on the parent feature.                                       
![view_fe](https://cloud.githubusercontent.com/assets/12252068/22693198/e8943f64-ed4a-11e6-9bbb-01a30251c175.png)

2. Click on Git Flow
![gitflow](https://cloud.githubusercontent.com/assets/12252068/22692868/8e6e030e-ed49-11e6-8fb5-c424f54df136.png)

3.	The following screen will appear click on **Other Actions**,Then click on **Start New Feature**.                                             
![new fe](https://cloud.githubusercontent.com/assets/12252068/22693084/864756b6-ed4a-11e6-8e1a-c873e1f380b1.jpg)

4.	Type Feature Name in the appeared window following this format “Child_Feature_Name”, Select **Working copy parent** Option and click Ok.                                          
![child_fe](https://cloud.githubusercontent.com/assets/12252068/22693404/d00f1256-ed4b-11e6-9d26-c1263c54b9bb.png)

5.	The feature “Child_Feature_Name” is successfully created out of “Feature_Name” Feature.                                   
![child_v](https://cloud.githubusercontent.com/assets/12252068/22693425/e9a3f9fc-ed4b-11e6-82cb-6388ea212d77.png)


## Start New Hotfix
1. Switch to develop branch.
2. Click on Git Flow.                                     
![gitflow](https://cloud.githubusercontent.com/assets/12252068/22692868/8e6e030e-ed49-11e6-8fb5-c424f54df136.png)

3.	Click on **Start new hotfix**.                                                      
![newhot](https://cloud.githubusercontent.com/assets/12252068/22693493/37bb131e-ed4c-11e6-9e90-34e79a2374c2.png)

4.	Write your HotFix Name.                                            
![hotname](https://cloud.githubusercontent.com/assets/12252068/22693533/558a12b4-ed4c-11e6-907f-595dad80bd3d.png)

5.	The hotfix name will be created successfully when you have latest of your master branch 

## Commit Messages

**ENHANCEMENT:** For Enhancing and code refactoring.

**UPDATE:** Adding new code.

**MAINTENANCE:** Update an existing code or fixing an error without an opened defect.

**DEFECT:** For Fixing Defects
## Create Pull Request
1. Push your code to the feature you are working on.
2. Click on **Create pull request** from repository tab.
![create](https://cloud.githubusercontent.com/assets/12252068/22693895/cab50fa2-ed4d-11e6-8001-db8c002e1c23.png)

3. The following screen will appear, Click on Create pull request on web.                             
![on web](https://cloud.githubusercontent.com/assets/12252068/22693927/eb741eea-ed4d-11e6-94fa-51d2fee954c9.png)

4. You will be redirected to the following Github Page.                                
![pull](https://cloud.githubusercontent.com/assets/12252068/22693974/1a1fdea0-ed4e-11e6-9d80-3485ba98e84a.png)

* Make sure that the base branch is the sprint branch.

* The Branch is able to merge and has no conflicts.

* You assigned the pull request to the one responsible for reviewing your code.

5. Click on **Create pull request** button.

## Code Review Checklist

- [x] Make sure that the base branch is the sprint branch.
- [x] Make sure that the code follows the best practices defined in the development guide.
- [x] Make sure that the feature to be merged has no conflicts with the base branch.

