# Data Generation For RadX Signatures

This repo is used in conjunction with Nextstrain's ncov to generate SARS-CoV-2 builds for
use with the RadX DCC Signatures panel.  Steps to use (following [the ncov tutorial]):

- `git clone https://github.com/nextstrain/ncov.git`, then `cd ncov`
- create a local branch (name of choosing)
- modify the file `workflow/snakemake_rules/main_workflow.smk`
  - add `--include-root-sequence` under the `augur export` args
- still in `ncov`, `git clone https://github.com/center4health/radx-signatures-data.git`
- `nextstrain build . --configfile radx-signatures-data/variants-data.yaml`
- go get a cup of coffee
- test with `nextstrain view auspice/`

## What this does

- in the variants-data.yaml are explicit instructions for generating the dataset
  - downloads a curated set of 100k covid samples from genbank, plus the Wuhan reference
  - filters out sequences with `clade_who == 'recombinant'` and those with missing data
  - subsamples to select 10 sequences from each who variant
- in auspice-config-variants.json are instructions for coloring by variant

## Path Note

File paths in the [config files] must start with the [analysis directory]. For example, in the tutorial:

```yaml
auspice_config: radx-signatures-data/auspice-config-variants.json
```

[config files]: https://docs.nextstrain.org/projects/ncov/en/latest/guides/workflow-config-file.html
[analysis directory]: https://docs.nextstrain.org/projects/ncov/en/latest/reference/glossary.html#term-analysis-directory
[the ncov tutorial]: https://docs.nextstrain.org/projects/ncov/en/latest/index.html
