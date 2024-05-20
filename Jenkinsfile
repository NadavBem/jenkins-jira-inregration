pipeline {
    agent any

    environment {
        JIRA_SITE = 'nadav jira' // Jenkins Jira configuration name
    }
    stages {
        stage('Check Pull Request') {
            when {
                allOf {
                    branch 'main'
                    expression {
                        def branchName = env.CHANGE_BRANCH
                        def jiraIssueKey = env.CHANGE_BRANCH // Assuming branch name is JIRA issue key
                        return branchName == jiraIssueKey
                    }
                }
            }
            steps {
                script {
                    def jiraIssueKey = env.CHANGE_BRANCH
                    echo "Branch name matches JIRA issue key: ${jiraIssueKey}"
                    
                    jiraTransitionIssue idOrKey: jiraIssueKey, transition: 'Done', site: env.JIRA_SITE
                    echo "JIRA issue ${jiraIssueKey} transitioned to 'Done'"
                }
            }
        }
    }
}


// node {
//   stage('Move Issue to Done') {
//     withEnv(['JIRA_SITE=nadav jira']) {
//       def transitionInput =
//       [
//           transition: [
//               id: '31'
//           ]
//       ]

//       jiraTransitionIssue idOrKey: 'JEN-1', input: transitionInput
//     }
//   }
// }
