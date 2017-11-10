# Machine Learning Engineer Nanodegree
## Predicting the Value of Ether over Time
Stephanie Marker
November 10, 2017

## I. Definition

### Project Overview

### Domain Background

Ethereum is a decentralized digital cryptocurrency platform invented by Vitalik Buterin in 2013. It uses public key cryptography and a consensus algorithm called "proof of work" (POW) to prevent denial of service attacks on the system. [1](https://github.com/ethereum/wiki/wiki/White-Paper) Ether, Ethereum’s currency, does not go through a bank, rather, Ether are managed in peer to peer transactions. Therefore Ether transactions are much cheaper.
Transactions are tracked on the blockchain, a distributed ledger. As Figure 1 indicates, every block in the chain contains a pointer from the previous block, a timestamp, a nonce, and a copy of valid transaction records within that block.

![blockchain components](https://cdn-images-1.medium.com/max/1600/1*W-8mmfDDP5jrPMtsJSa0Rw.png)

**Figure 1** [2](https://en.wikipedia.org/wiki/Blockchain)
When a person wants to send Ether to another user, that person will request to have their transaction be validated by the miners and added to the chain.[2](https://spectrum.ieee.org/computing/networks/the-future-of-the-web-looks-a-lot-like-bitcoin) Each miner maintains their own copy of the blockchain, so that they can verify each other's work. Miners race to validate these requests. The miner with the longest chain and a majority approval from the other miners working on their own copies of the chain receives a monetary reward in Ether for the transactions that the miner verified. Only when the miners are in agreement, does the transaction get added to the latest block in their copy of the chain.  
Because blockchain is peer to peer and relies on proof of work, it deters people from attempting to alter the history of transactions. This is because a crook would have to fool the other miners that their copy of the chain with an altered beginning transaction is valid. Remember, the miner who has the longest verified chain has their chain accepted as the source of truth for all the other miners. Therefore, a crook would have to do expensive calculations from the early block to the current block faster than all the other miners compute the current block as shown in Figure 2.

![blockchain security](https://spectrum.ieee.org/img/07OLBitcoinf2-1435160570777.png)

**Figure 2** [3](https://spectrum.ieee.org/img/07OLBitcoinf2-1435160570777.png) 
The more people that use Ether, the more valuable it is, as increased use validates its acceptance in the community. You can see this effect in Figure 3, as the number of transactions of Ether have increased over time, with the largest number of transactions, 546,837, occurring on Friday, October 20, 2017. This increased transaction count is correlated to the price of Ether as evident when comparing the price of Ether in Figure 4 with its transaction count in Figure 3.

[add pic here]

Figure 3 [4](https://etherscan.io/chart/tx)

[add pic here]

Figure 4 [5](https://cointelegraph.com/ethereum-price-index)
I want to analyze the price of Ether over time because it is gaining popularity and I personally believe in this product.

### Problem Statement
The goal of this project is to predict the daily closing prices of Ether for a week into the future. This can be solved with supervised learning since at least a year of data exists with several labels like address, block size, ether price, etc. In addition, I would like to use github contribution history to see if more contributions also influence the price, as I expect more frequent, larger contributions would increase Ether price as the Ethereum framework gets more robust.

**To solve this problem I would like to take these steps:**

1. Using Kaggle Ethereum data as a base (Kaggle data was taken from Etherscan), fill in newer Ethereum data using data extracted from Etherscan. Filter out any Ethereum data prior to March 2017.
2. Create a python script to extract commits with [GitHub's GraphQL API](https://developer.github.com/v4/) from Ethereum's [Go Client](https://github.com/ethereum/go-ethereum), [Rust Client](https://github.com/paritytech/parity), and [C++ Client](https://github.com/ethereum/cpp-ethereum).
3. Merge the etherscan data with ethereum commit history data using a pandas dataframe.
4. Split the dataframe into two dataframes, X, which contains the features, and y, which contains the values I would like to predict.
4. Normalize the data before performing PCA.
5. Perform PCA to determine what features are most relevant to my predictions. 
6. Divide the data into training and testing data. I would not shuffle the data since I am working with time series data so I will use TimeSeriesSplit. 
7. Train with multiple ML models to see which one best captures the data. I will try with bayesian linear regression using scikit learn’s Bayesian Ridge regression, Long Short-Term (LSTM) Time-Series recurrent neural network (RNN), and an ARIMA model. As I train I would tune the hyperparameters. 
8. Predict the price for the next 7 days. 
9. Print the results and the mean squared error as my evaluation metric.

[anticipated solution and expected results]

### Metrics
In this section, you will need to clearly define the metrics or calculations you will use to measure performance of a model or result in your project. These calculations and metrics should be justified based on the characteristics of the problem and problem domain. Questions to ask yourself when writing this section:
- _Are the metrics you’ve chosen to measure the performance of your models clearly discussed and defined?_
- _Have you provided reasonable justification for the metrics chosen based on the problem and solution?_


## II. Analysis
_(approx. 2-4 pages)_

### Data Exploration
In this section, you will be expected to analyze the data you are using for the problem. This data can either be in the form of a dataset (or datasets), input data (or input files), or even an environment. The type of data should be thoroughly described and, if possible, have basic statistics and information presented (such as discussion of input features or defining characteristics about the input or environment). Any abnormalities or interesting qualities about the data that may need to be addressed have been identified (such as features that need to be transformed or the possibility of outliers). Questions to ask yourself when writing this section:
- _If a dataset is present for this problem, have you thoroughly discussed certain features about the dataset? Has a data sample been provided to the reader?_
- _If a dataset is present for this problem, are statistics about the dataset calculated and reported? Have any relevant results from this calculation been discussed?_
- _If a dataset is **not** present for this problem, has discussion been made about the input space or input data for your problem?_
- _Are there any abnormalities or characteristics about the input space or dataset that need to be addressed? (categorical variables, missing values, outliers, etc.)_

### Exploratory Visualization
In this section, you will need to provide some form of visualization that summarizes or extracts a relevant characteristic or feature about the data. The visualization should adequately support the data being used. Discuss why this visualization was chosen and how it is relevant. Questions to ask yourself when writing this section:
- _Have you visualized a relevant characteristic or feature about the dataset or input data?_
- _Is the visualization thoroughly analyzed and discussed?_
- _If a plot is provided, are the axes, title, and datum clearly defined?_

### Algorithms and Techniques
In this section, you will need to discuss the algorithms and techniques you intend to use for solving the problem. You should justify the use of each one based on the characteristics of the problem and the problem domain. Questions to ask yourself when writing this section:
- _Are the algorithms you will use, including any default variables/parameters in the project clearly defined?_
- _Are the techniques to be used thoroughly discussed and justified?_
- _Is it made clear how the input data or datasets will be handled by the algorithms and techniques chosen?_

### Benchmark
A team of MIT students used bayesian regression to predict every two seconds, the average price change of Bitcoin over the next 10 seconds. The team was successful and “over 50 days, the team’s 2,872 trades gave them an 89 percent return on investment.” [12](http://news.mit.edu/2014/mit-computer-scientists-can-predict-price-bitcoin) They wrote a paper on their Bayesian regression method and how effectively they predicted the price of Bitcoin, a cryptocurrency. [13](https://dspace.mit.edu/handle/1721.1/101044)

## III. Methodology
_(approx. 3-5 pages)_

### Data Preprocessing
In this section, all of your preprocessing steps will need to be clearly documented, if any were necessary. From the previous section, any of the abnormalities or characteristics that you identified about the dataset will be addressed and corrected here. Questions to ask yourself when writing this section:
- _If the algorithms chosen require preprocessing steps like feature selection or feature transformations, have they been properly documented?_
- _Based on the **Data Exploration** section, if there were abnormalities or characteristics that needed to be addressed, have they been properly corrected?_
- _If no preprocessing is needed, has it been made clear why?_

### Implementation
In this section, the process for which metrics, algorithms, and techniques that you implemented for the given data will need to be clearly documented. It should be abundantly clear how the implementation was carried out, and discussion should be made regarding any complications that occurred during this process. Questions to ask yourself when writing this section:
- _Is it made clear how the algorithms and techniques were implemented with the given datasets or input data?_
- _Were there any complications with the original metrics or techniques that required changing prior to acquiring a solution?_
- _Was there any part of the coding process (e.g., writing complicated functions) that should be documented?_

### Refinement
In this section, you will need to discuss the process of improvement you made upon the algorithms and techniques you used in your implementation. For example, adjusting parameters for certain models to acquire improved solutions would fall under the refinement category. Your initial and final solutions should be reported, as well as any significant intermediate results as necessary. Questions to ask yourself when writing this section:
- _Has an initial solution been found and clearly reported?_
- _Is the process of improvement clearly documented, such as what techniques were used?_
- _Are intermediate and final solutions clearly reported as the process is improved?_


## IV. Results
_(approx. 2-3 pages)_

### Model Evaluation and Validation
In this section, the final model and any supporting qualities should be evaluated in detail. It should be clear how the final model was derived and why this model was chosen. In addition, some type of analysis should be used to validate the robustness of this model and its solution, such as manipulating the input data or environment to see how the model’s solution is affected (this is called sensitivity analysis). Questions to ask yourself when writing this section:
- _Is the final model reasonable and aligning with solution expectations? Are the final parameters of the model appropriate?_
- _Has the final model been tested with various inputs to evaluate whether the model generalizes well to unseen data?_
- _Is the model robust enough for the problem? Do small perturbations (changes) in training data or the input space greatly affect the results?_
- _Can results found from the model be trusted?_

### Justification
In this section, your model’s final solution and its results should be compared to the benchmark you established earlier in the project using some type of statistical analysis. You should also justify whether these results and the solution are significant enough to have solved the problem posed in the project. Questions to ask yourself when writing this section:
- _Are the final results found stronger than the benchmark result reported earlier?_
- _Have you thoroughly analyzed and discussed the final solution?_
- _Is the final solution significant enough to have solved the problem?_


## V. Conclusion
_(approx. 1-2 pages)_

### Free-Form Visualization
In this section, you will need to provide some form of visualization that emphasizes an important quality about the project. It is much more free-form, but should reasonably support a significant result or characteristic about the problem that you want to discuss. Questions to ask yourself when writing this section:
- _Have you visualized a relevant or important quality about the problem, dataset, input data, or results?_
- _Is the visualization thoroughly analyzed and discussed?_
- _If a plot is provided, are the axes, title, and datum clearly defined?_

### Reflection
In this section, you will summarize the entire end-to-end problem solution and discuss one or two particular aspects of the project you found interesting or difficult. You are expected to reflect on the project as a whole to show that you have a firm understanding of the entire process employed in your work. Questions to ask yourself when writing this section:
- _Have you thoroughly summarized the entire process you used for this project?_
- _Were there any interesting aspects of the project?_
- _Were there any difficult aspects of the project?_
- _Does the final model and solution fit your expectations for the problem, and should it be used in a general setting to solve these types of problems?_

### Improvement
In this section, you will need to provide discussion as to how one aspect of the implementation you designed could be improved. As an example, consider ways your implementation can be made more general, and what would need to be modified. You do not need to make this improvement, but the potential solutions resulting from these changes are considered and compared/contrasted to your current solution. Questions to ask yourself when writing this section:
- _Are there further improvements that could be made on the algorithms or techniques you used in this project?_
- _Were there algorithms or techniques you researched that you did not know how to implement, but would consider using if you knew how?_
- _If you used your final solution as the new benchmark, do you think an even better solution exists?_

-----------

**Before submitting, ask yourself. . .**

- Does the project report you’ve written follow a well-organized structure similar to that of the project template?
- Is each section (particularly **Analysis** and **Methodology**) written in a clear, concise and specific fashion? Are there any ambiguous terms or phrases that need clarification?
- Would the intended audience of your project be able to understand your analysis, methods, and results?
- Have you properly proof-read your project report to assure there are minimal grammatical and spelling mistakes?
- Are all the resources used for this project correctly cited and referenced?
- Is the code that implements your solution easily readable and properly commented?
- Does the code execute without error and produce results similar to those reported?

Datasets
#### From Kaggle
* `ethereum_dataset.csv`

#### From GitHub GraphQL API v4
* `github_commit_history.graphql` - gets the commit history of the go-ethereum repository
* `github_commit_history_response.json` - example response from github_commit_history.graphql

To test the query live, you can navigate to `https://developer.github.com/v4/explorer/`.

For the capstone, I will be writing a python script to get commits aggregated from the top 3 ethereum client github repositories from March 2017 to present day.

The script will format the data a csv as such (similar to ethereum_dataset.csv):
```
Date (UTC) | total_commits
3/1/2017   | 5
3/2/2017   | 3
...
```

## Proposal
* proposal.pdf
