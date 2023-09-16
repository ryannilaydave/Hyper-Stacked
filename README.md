# Hyper-Stacked
 Hyper-Stacked: A Scalable and Distributed Approach to Automated Machine Learning. First Author Publication by Springer in the ‘International Cross-Domain Conference for Machine Learning and Knowledge Extraction’

# Usage
## Initialise HyperStacked
val hyperStacked = new HyperStacked(
  inputCol = "<prediction_column>",
  optL1 = true
)

## Load training data
val trainValid = Logger.log(hyperStacked.load(spark,"/mnt/<blob_storage>/<train_dataset>.parquet"), "Training data load time")

## Train model
val model = Logger.log(hyperStacked.fit(trainValid), "Model fit time")

## Load test data
val test = Logger.log(hyperStacked.load(spark,"/mnt/<blob_storage>/<test_dataset>.parquet"), "Test data load time")

## Predict on test data
val output = model.transform(test)

## Evaluate using chosen metric
val roc = model.evaluate(output, "areaUnderROC")

## Show leaderboard (optional) 
model.getLeaderBoard(test, "areaUnderROC").foreach(println)
