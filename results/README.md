# Recorded results

These files were transcribed or extracted from the submitted notebook, not produced by a new run.

- `recorded_metrics.csv`: rounded metrics printed in the original output. The internal report describes the last epoch; it does not independently re-evaluate the restored checkpoint.
- `recorded_validation_confusion_matrix.csv`: counts from the 82-image course-provided validation set. Rows are true classes and columns are predicted classes.
- `recorded_test_predictions.csv`: 149 labels in the original printed order, with a header added for readability. There is no complete saved filename manifest, so filenames have not been reconstructed. This is not the header-free coursework submission CSV.
- `original_stdout.txt`: original console output, retained as an audit trail. Historical paths and wording are unchanged here.
- `../figures/*_original.png`: exact PNG bytes extracted from saved notebook outputs. No figures were recalculated.

The unlabeled test set has 59 predictions of normal tissue and 90 predictions of invasive carcinoma. These are prediction counts, not measured test performance. Future executions write separate files to `results/generated/`.
