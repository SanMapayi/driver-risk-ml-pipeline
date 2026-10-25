# Driver Risk ML Pipeline

An MSc project at the University of York exploring driver-risk classification from vehicle telemetry using Java, DeepLearning4J, DataVec, and ND4J.

## Pipeline

~~~text
raw CSV -> cleaning -> train/test split -> data iterators
        -> neural-network training -> evaluation -> saved model and charts
~~~

The project includes single-event and batch prediction entry points, trip-level aggregation, and experiment comparison utilities. The target label is anomalous_event: 0 means safe and 1 means risky in the dataset.

## Build

Requires JDK 23 or newer and Maven. The first build downloads native ND4J dependencies and can be large.

~~~sh
mvn -B compile
~~~

## Run

Run commands from the repository root. Place the input CSV at:

~~~text
dataset/raw/driver_behavior_route_anomaly_dataset_with_derived_features.csv
~~~

~~~sh
mvn exec:java "-Dexec.mainClass=uk.ac.york.driverriskpredictivemodel.app.main"
mvn exec:java "-Dexec.mainClass=uk.ac.york.driverriskpredictivemodel.app.DemoPredictor"
mvn exec:java "-Dexec.mainClass=uk.ac.york.driverriskpredictivemodel.app.BatchPredictor"
~~~

The training class is named lowercase main in the existing source. The training entry point reuses processed train/test files when present and loads the saved model when available, so a rerun is not automatically a fresh experiment. Review and archive the existing artifacts before choosing to regenerate them.

Paths are centralised in GlobalVariables. Prediction entry points also have their own input assumptions; inspect those before supplying a different dataset.

## Source map

| Package | Responsibility |
|---|---|
| data | Loading, cleaning, splitting, and transformation |
| model | Network configuration, training, evaluation, persistence |
| app | Training and prediction entry points |
| util | Charts, confusion matrices, and experiment comparisons |

Experiment outputs are under docs/experiments; the saved model is under dataset. Results belong to a specific dataset, split, and training run. No accuracy claim is made here without the corresponding experiment evidence.

## Evaluation limitations

This is a research prototype. Its predictions are not a validated assessment of an individual driver's safety. Dataset provenance, leakage prevention, class balance, split strategy, and threshold selection affect how results should be interpreted.

See [the reproducibility checklist](docs/reproducibility.md).