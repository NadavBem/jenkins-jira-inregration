pipeline {
    agent any

    environment {
        JIRA_SITE = 'nadav jira' // Jenkins Jira configuration name
    }

    stages {
        stage('Extract Branch Name and Transition Issue') {
            steps {
                script {
                    // Extract the branch name from the merge commit message
                    def commitMessage = sh(script: 'git log -1 --pretty=%B', returnStdout: true).trim()
                    echo "Commit message: ${commitMessage}"

                    // Assuming the branch name is the second part of the message, e.g., "Merge pull request #5 from branch_name"
                    def branchName = commitMessage.split('/')[2]
                    echo "Extracted branch name: ${branchName}"

                    // Define the transition input for the Jira issue
                    def transitionInput = [
                        transition: [
                            id: '31' // Replace with the actual transition ID for "Done"
                        ]
                    ]

                    // Perform the Jira issue transition using the extracted branch name as the issue key
                    jiraTransitionIssue idOrKey: branchName, input: transitionInput, site: env.JIRA_SITE
                    echo "JIRA issue ${branchName} transitioned to 'Done'"
                }
            }
        }
    }
}

