# QA-All

**Hugging Face Repositories**:
- [expansio/qa-wikipedia](https://huggingface.co/datasets/expansio/qa-wikipedia)
- [expansio/qa-nkjp](https://huggingface.co/datasets/expansio/qa-nkjp)
- [expansio/qa-kpwr](https://huggingface.co/datasets/expansio/qa-kpwr)

## Description

QA-All is the joint evaluation suite that bundles the three Polish extractive question answering datasets released by Expansio Software House - QA-Wikipedia, QA-NKJP and QA-KPWr - and reports scores aggregated across all three sources. The three component datasets share a common schema and a SQuAD 2.0-style task definition, which lets a single model be trained once and evaluated against a domain-diverse Polish QA benchmark covering encyclopedic text (Wikipedia), mixed-genre national corpus material (NKJP) and the multi-domain KPWr corpus.

The `qa_all` slug is an **evaluation aggregate** used by the LEPISZCZE leaderboard; it is not a separate Hugging Face dataset. To reproduce the benchmark, load each component dataset from Hugging Face, evaluate a model on each `validation` split, and report metrics on the concatenation.

## Tasks (input, output and metrics)

Extractive question answering with unanswerable questions.

**Input** (`question` + `context` columns): a Polish question and a passage from one of the three source corpora.

**Output**: a character-level span inside `context`, or an abstention when no answer is present.

**Measurements**: SQuAD 2.0 metrics - `exact`, `f1`, `HasAns_exact`, `HasAns_f1`, `NoAns_f1` - reported on the concatenated validation set.

## Data splits

| Component      | train  | validation |
|----------------|-------:|-----------:|
| QA-Wikipedia   |  6,458 |      1,639 |
| QA-NKJP        |  4,417 |        908 |
| QA-KPWr        |  7,563 |      1,878 |
| **QA-All**     | **18,438** | **4,425** |

## Schema

All three component datasets share the same schema:

| Column          | Type                                                 | Description                                                            |
|-----------------|------------------------------------------------------|------------------------------------------------------------------------|
| `question`      | string                                               | Question text in Polish                                                |
| `context`       | string                                               | Source passage (Wikipedia / NKJP / KPWr)                               |
| `answers`       | {`answer_start`: int[], `answer_end`: int[], `text`: string[]} | Answer spans; `null` when `is_impossible` is true            |
| `is_impossible` | bool                                                 | `true` if the question cannot be answered from `context`               |
| `is_paraphrase` | bool                                                 | `true` if the question is a paraphrase of another item on this context |
| `dataset`       | string                                               | Source identifier (`wikipedia` / `NKJP` / `KPWR`)                      |
| `context_id`    | int64                                                | Shared id of all questions for the same context                        |

## License

TBD - per-component licenses follow upstream corpora; see the individual dataset pages.

## Links

[QA-Wikipedia](https://huggingface.co/datasets/expansio/qa-wikipedia)

[QA-NKJP](https://huggingface.co/datasets/expansio/qa-nkjp)

[QA-KPWr](https://huggingface.co/datasets/expansio/qa-kpwr)

[Expansio Software House](https://expans.io)

[CLARIN-PL](https://clarin-pl.eu/)

## Examples

### Loading the joint validation set

```python
from datasets import load_dataset, concatenate_datasets

components = ["expansio/qa-wikipedia", "expansio/qa-nkjp", "expansio/qa-kpwr"]
validation = concatenate_datasets(
    [load_dataset(name, split="validation") for name in components]
)
print(len(validation))  # 4425
```

### Training across all three sources

```python
from datasets import load_dataset, concatenate_datasets

train = concatenate_datasets(
    [
        load_dataset(name, split="train")
        for name in ("expansio/qa-wikipedia", "expansio/qa-nkjp", "expansio/qa-kpwr")
    ]
)
print(len(train))  # 18438
```
