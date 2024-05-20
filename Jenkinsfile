pipeline {
    agent any

    environment {
        JIRA_SITE = 'nadav jira' // Jenkins Jira configuration name
    }

    triggers {
        githubPullRequest()
    }

    stages {
        stage('Print Environment Variables') {
            steps {
                script {
                    echo "CHANGE_BRANCH: ${env.CHANGE_BRANCH}"
                    echo "CHANGE_TARGET: ${env.CHANGE_TARGET}"
                    echo "BRANCH_NAME: ${env.BRANCH_NAME}"
                }
            }
        }
        
        stage('Check Pull Request') {
            when {
                allOf {
                    branch 'main'
                    expression {
                        def branchName = env.CHANGE_BRANCH ?: env.BRANCH_NAME
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
