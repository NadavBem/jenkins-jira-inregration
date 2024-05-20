node {
  stage('Move Issue to Done') {
    withEnv(['JIRA_SITE=nadav jira']) {
      def transitionInput =
      [
          transition: [
              id: '31'
          ]
      ]

      jiraTransitionIssue idOrKey: 'JEN-1', input: transitionInput
    }
  }
}
