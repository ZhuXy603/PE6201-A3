# PE6201 End of Course Project

Evidence-grounded Apple product support assistant using a corrected, source-attributed Singapore-focused corpus.

## Contents

- `run_project.py`: local retrieval comparison and optional OpenRouter answer generation.
- `data/Part2_notebook.ipynb`: current 10-note source-attributed corpus read by the runner.
- `audit/Part2_classroom_original_invalidated.ipynb`: old classroom corpus, audit only; not used by the runner.
- `sources.md`: official source register and corrected claims.
- `data_plan.md`: provenance and limits.
- `evaluation_plan.md`: fixed 10-case set, scoring method and current evaluation status.
- `audit/top_k_comparison_classroom_invalidated.csv`: invalidated old output, audit only; do not use its metrics.
- `results/top_k_comparison_first_scored_run.csv`: first corrected-corpus run before prompt revision.
- `results/top_k_comparison_final_prompt_run.csv`: current revised-prompt run and raw model outputs.
- `results/run_metadata.json`: recorded run details, token totals and explicitly qualified cost estimate.
- `results/evidence_audit.csv`: automated Evidence format and source-ID checks.
- `audit_outputs.py` / `results/l1_heuristic_audit.csv`: repeatable literal required-term and forbidden-phrase flags (heuristic only; run `python3 audit_outputs.py` from this folder).
- `evaluation_results.csv`: merged raw answers, manual strict/refusal judgments and citation checks for row-by-row review.
- `problem_statement.md` and `product_documentation.md`: project documentation.
- `video.mov`: recorded demo video.
- `final_report.pdf`: formatted report for submission.

## Run retrieval without API calls

From this folder:

```bash
python3 run_project.py --dry-run
```

This reads the corrected corpus and writes retrieval-only rows to `results/top_k_comparison.csv`. The fallback may use TF-IDF if `sentence-transformers` is not installed. A dry run does not measure answer correctness or reproduce historical semantic-model results.

## Run answer evaluation

Install the full evaluation dependencies from this folder (`pip install -r requirements.txt`), set an OpenRouter key in the environment, and run:

```bash
OPENROUTER_API_KEY="your-key" python3 run_project.py
```

This makes 20 model calls (10 questions × 2 k settings) and writes `results/top_k_comparison.csv`. API cost depends on provider/model. Review each answer manually using `evaluation_plan.md`; the script does not grade correctness. Do not overwrite the old audit file with this run. Never commit an API key.

## Evaluation status

The previous classroom scores were withdrawn. The revised-prompt run retrieved 10/10 required notes, scored 7/10 strict answers at k=1 and 8/10 at k=2, and passed 3/3 refusal cases at each setting. The ≥80% strict target was missed at k=1 and met at k=2. Both Trade In answers omit the condition-match qualifier. The run used local semantic embeddings. The code default is `qwen/qwen-2.5-7b-instruct`, but the historical run did not record whether `PE6201_MODEL` overrode it; see `results/run_metadata.json` for this uncertainty and the conditional cost estimate. The folder contains `video.mov` (7:05). Confirm that your final ZIP includes the required project files and does not contain an API key.
