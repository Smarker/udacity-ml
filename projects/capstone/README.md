# Capstone Proposal

## Datasets
#### From Kaggle
* ethereum_dataset.csv

#### From GitHub GraphQL API v4
* github_commit_history.graphql - gets the commit history of the go-ethereum repository
* github_commit_history_response.json - example response from github_commit_history.graphql

To test the query live, you can navigate to `https://developer.github.com/v4/explorer/`.

For the capstone, I will be writing a python script to get commits from the top 3 ethereum client github repositories from March 2017 to present day.

The data will be formatted as a csv as such (similar to ethereum_dataset.csv):
```
Date (UTC) | total_commits
3/1/2017  | 5
3/2/2017  | 3
...
```

## Proposal
* proposal.pdf
