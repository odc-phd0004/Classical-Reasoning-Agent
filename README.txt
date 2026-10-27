Files
-----
main.ipynb              complete implementation, evaluation, experiments and reasoning traces
submission.csv          predictions (columns: id, label) produced by the notebook
report.pdf

Requirements
------------
Python 3.10+ with pandas, numpy and pyarrow (for reading .parquet).
No other libraries, no GPU, no internet and no trained model are needed.

Data layout (relative to the notebook)
--------------------------------------
data/ruletaker/     RuleTaker test split   (tasksource/ruletaker, test-*.parquet)
data/counterbench/  data_balanced_alpha_V1.json, data_balanced_backdoor_V2.json  (CounterBench/CounterBench)
data/folio/         folio_v2_train.jsonl, folio_v2_validation.jsonl  (yale-nlp/FOLIO)

How to run
----------
Open reasoning_agent.ipynb and run all cells (Kernel > Restart & Run All).
The notebook prints the final accuracy and total inference time, the per-dataset and per-group
results, the experiments, example reasoning traces, and writes submission.csv.

Private test set
----------------
Put the test file at data/test.csv with columns: id, context, statement.
The last cell then predicts every row with predict(context, statement) and writes
submission.csv with columns id, label (True / False). Without data/test.csv the file is
produced for the public evaluation queries.

Single query
------------
predict(context, statement) -> True / False
  e.g. predict("Bob is young. Bob is kind. If someone is young, then they are smart. "
               "If someone is smart and kind, then they are successful.", "Bob is successful.")  -> True
For FOLIO-style input the FOL annotations can be passed as well:
  predict(context, statement, fol_premises=[...], fol_conclusion="...")

Results on the public data (from the notebook)
----------------------------------------------
see the summary table printed in section 7 of the notebook and in report.pdf.
