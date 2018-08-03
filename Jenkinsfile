import com.cwctravel.hudson.plugins.extended_choice_parameter.ExtendedChoiceParameterDefinition

properties([parameters([string(defaultValue: '', description: '', name: 'SHA', trim: true), string(defaultValue: 'release', description: '', name: 'ReleaseBranchName', trim: true)])])


node {
def multiSelect= new ExtendedChoiceParameterDefinition("action", 
            "PT_CHECKBOX", 
            "merge,artifactoryMove,revup,releasenote,EXTRA1,EXTRA2", 
            "project name",
            "", 
            "",
            "", 
            "", 
            "", 
            "", 
            "artifactoryMove,EXTRA1,EXTRA2", 
            "", 
            "", 
            "", 
            "", 
            "", 
            "", 
            "", 
            "", 
            "", 
            "", 
            "", 
            "", 
            "", 
            "", 
            "", 
            false,
            false, 
            8, 
            "multiselect", 
            ",") 
    def action = ""
   try {
       timeout(time: 10, unit: 'SECONDS') {
           action = input  id: 'customID', message: 'Choose your action', ok: 'Release!', parameters:  [multiSelect]
        }
   }
    catch(e) {
        echo "timeout! so use the default"
        action = "artifactoryMove,EXTRA1,EXTRA2"
    }
  stage('Create branch') {
    if (env.BRANCH_NAME == 'master') {
        echo 'Master branch flow'
        sh 'echo "Calling create branch bacon task with branchname ${ReleaseBranchName}"'
    } else {
        echo 'Not master branch. doing something else?'
        echo "branchname is ${ReleaseBranchName}"
    }
    
    echo "my actions are ${action}"
    
  }

  stage('artifactoryMove') {
      if (action.contains("artifactoryMove")) {
              echo "doing artifactory move"
              echo "bacon task"
              echo "SHA is ${SHA}"

      }
      else {
              echo "SKIPPING artifactory move"

      }
  }
  
  stage('revup') {
      if (action.contains("revup")) {
              echo "doing some revup"

      }
      else {
              echo "SKIPPING some revup"

      }
  }

  stage('releaseNote') {
    echo "doing release note"
    echo "calling a bacon task for release note"
  }

}
