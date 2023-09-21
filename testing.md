This guideline explains the testing approach within the edunota project.

a. For every new feature/business logic some unit test should be added.
-for backend repo: testify framework: https://github.com/stretchr/testify

b. All unit tests should pass in order to commit (pre-commit hooks).

c. Code coverage should be updated with merge and discussed at the end of the sprints.

d. e2e testing is the testing (in the order of) database-backend-frontend. framework: https://www.cypress.io

e. Integration test is testing between database and backend. framework: https://www.postman.com (mock servers)
