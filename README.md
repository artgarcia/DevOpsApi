# DevOpsApi
PowerShell to work with Azure DevOps API
These PowerSHell scripts are designed to facilitate working with the Azure DevOps envorinment using the published API's
</br>
</br>
The scripts contain the following modules:
</br>
</br>

1 - WiKiMain.ps1 - This module will generate release notes and publish them into a given Azure DevOps WiKi.
      By simply tagging a build or builds, these scripts will generate all the changes to a build, all work items checked in,
      a list of builds tagged and any artifacts for the tagged builds.
</br>
</br>
      Variables Required

              In order to run the Release Notes generation script you will need to set a few variables. These variables are found in the ProjectDef.json file. 
              Following are the variable you will need to review prior to running the script. NOTE only replace data within the quotes. DO NOT REMOVE any of the COMMAs.

              "VSTSMasterAcct" : "Org name",
              "userEmail"      : "your email address",
              "PAT"            : "this is where you add your Personal access token (PAT) ",       
              "ProjectName"    : "project name",      - THIS IS THE NAME OF THE PROJECT YOU WANT TO REPORT ON

              "BuildTags"      : "Release:1.1.0",     - THIS IS THE RELEASE YOU WANT TO REPORT ON. NOTE IT MUST BE IN THE FORMAT SHOWN
                                                          :Release:x.x.x 

              "PublishWiKi"    : "lumina.wiki",           - THIS IS THE NAME OF THE WIKI TO PUBLISH TO 
              "PublishParent"  : "Release Notes",         - THIS IS THE PARENT PAGE THE PAGE WILL BE PLACED UNDER
              "PublishPagePrfx": "System Release ",       - THIS IS THE NAME YOU WANT FOR THE PAGE. NAME WIIL BE PROJECT NAME + THIS TAG 
                                                              + THE RELEASE NUMBER IE : fdx-surround - System Release - Release:1.1.0
              "PublishBldNote" : "Build section Notes",   - THIS IS ANY NOTES YOU WANT TO ADD TO THE BUILD SECTION
              "PublishWKItNote": "Work Item section note",- THIS IS ANY NOTES YOU WANT IN THE WORK ITEM SECTION

              "WorkItemTypes"  : ["User Story","Bug"],    - THESE ARE THE WORK ITEM TYPES TO REPORT ON . DO NOT CHANGE
              "BuildResults"   : ["Succeeded"],           - THIS IS THE BUILD STATUS TO REPORT ON. DO NOT CHANGE

              "HTTP_preFix"    : "https",                 - THIS IS THE SECURITY TO USE IN THE API CALL . DO NOT CHANGE
              "OutPutToFile"   : "No",                    - THIS IS IF YOU WANT LOGS GENERATED TO AUDIT WHAT GETS CREATED

              The above parameters are the only ones needed to run thr release notes. The file they reside in contains other parameters. PLEASE do not attemt to 
              change any other parameters without discussing it with the developer of this script.
      </br>

      Tagging of Azure DevOps artifacts. 

              In order for this script to work you must tag the builds you want included in the release notes. Each build you want to include in the Release Notes must 
              have a tag with the release number. This should be in the format of Release:x.x.x. Note PLEASE make sure that there are no spaces before or after any of 
              the peroids and before and after the :

              In summary the following tags must be present in each build you want in the release notes.
                  Release:x.x.x

</br>
</br>
2 - SecurityMain - This will generate a list of all users in a given project or orginization. 
                   It will also generate a list of all groups and teams in the given project or orginization.
                   It will list all the permissions for each group or team and the uesrs in each.
                   
</br>
</br>
3 - CreatMain.ps1 - This will generate a project,team and add users to a team. It will also create environments and default builds.
                    You can also create , List and delete branches in the Git Repos
                    There is also a function that allows you to copy processes and workItem Types within the process. You select the Process and WorkItem to copy from
                    and then the process and workItem to copy to.

                    Some other functions deal with getting repo information, copying deleting, etc. They are currently commented out, but feel free to use as needed.
                   
</br>
</br>
Execution process

        Step 1:
            Open the file to run. Open "Windows PowerShell ISE" as administrator and load the file to run.
            WikiMain.ps1, SecurityMain.ps1, or CreateMain.ps1
            
        Step 2: 
            Obtain a valid Personal Access Token. Refer to the documentation provided in the word doc on how to generate a token. 
            It is important that the token be a FULL Access token. Next add this token to the ProjectDef.Json file.

        Step 3:
            Modify the parameters for your project and release conditions. See (Variables Required above)
            We will begin by modifing the ProjectDef.json file as stated above in the Variables Required section. 
            This file contains the parameters needed to run the scripts. Review and modify each parameter as required making sure 
            you do not remove any COMMAS or Quotation marks.
                                     
        Step 4:
            Run the script. IF the page already exists the script will stop and generate an error message at the bottom of the page.
            the error will be : Page exists - Script terminated, Please review page

4 - WorkItemReleaseNotesMain.ps1 - This will generate release notes from a given shared query. It will take the first query and call it the current
                                   items and then a second query called future items. 
                                   
           To run tis script you must update the ProjectDef.json and update the following fields
           A - "CurrentWitemQry": "name of current query to use"
           B - "FutureWitemQry" : "name of future query"
           C - "PublishWiKi"    : "xxxxxxxxxxxxx.wiki"
           
           D -"VSTSMasterAcct" : "Org Name goes here"
           E- "userEmail"      : "user email address assocaited with pat key"
           F- "PAT"            : "pay key goes here"
           G - "ProjectName"   : "Project name goes here"
           H - "DefaultTeam"   : "default team name"   
          
           
</br>
</br>

