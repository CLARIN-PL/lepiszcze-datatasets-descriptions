# QA-Wikipedia

**Hugging Face Repository**: [expansio/qa-wikipedia](https://huggingface.co/datasets/expansio/qa-wikipedia)

## Description

QA-Wikipedia is a Polish extractive question answering dataset built on passages from Polish Wikipedia. Each example pairs a question written in Polish with a Wikipedia passage that may or may not contain the answer. The dataset follows a SQuAD 2.0-style format: answerable questions are accompanied by character-level answer spans, while unanswerable questions are flagged with `is_impossible=true` and carry no answer. A subset of questions are paraphrases of other items asked against the same context, which lets models be tested for robustness to surface-form variation.

## Tasks (input, output and metrics)

Extractive question answering with unanswerable questions.

**Input** (`question` + `context` columns): a Polish question and a Polish Wikipedia passage.

**Output**: a character-level span inside `context`, or an abstention when no answer is present.

**Measurements**: SQuAD 2.0 metrics - `exact`, `f1`, `HasAns_exact`, `HasAns_f1`, `NoAns_f1`.

**Example**:

Question: `Jak nazywał się autor, który stworzył najstarszy zapisek o smoku wawelskim?`

Context (excerpt): `...Najstarszy zachowany zapisek o smoku wawelskim pochodzi z kroniki Wincentego Kadłubka...`

Answer: `Wincenty Kadłubek.`

## Data splits

| Subset     | Cardinality (questions) |
|------------|------------------------:|
| train      |                   6,458 |
| validation |                   1,639 |
| test       |                       0 |

## Schema

| Column          | Type                                                 | Description                                                            |
|-----------------|------------------------------------------------------|------------------------------------------------------------------------|
| `question`      | string                                               | Question text in Polish                                                |
| `context`       | string                                               | Wikipedia passage                                                      |
| `answers`       | {`answer_start`: int[], `answer_end`: int[], `text`: string[]} | Answer spans; `null` when `is_impossible` is true            |
| `is_impossible` | bool                                                 | `true` if the question cannot be answered from `context`               |
| `is_paraphrase` | bool                                                 | `true` if the question is a paraphrase of another item on this context |
| `dataset`       | string                                               | Source identifier                                                      |
| `context_id`    | int64                                                | Shared id of all questions for the same context                        |

## License

TBD - source text from Polish Wikipedia (CC BY-SA 3.0).

## Links

[HuggingFace](https://huggingface.co/datasets/expansio/qa-wikipedia)

[Expansio Software House](https://expans.io)

[CLARIN-PL](https://clarin-pl.eu/)

## Examples

### Loading

```python
from pprint import pprint
from datasets import load_dataset

dataset = load_dataset("expansio/qa-wikipedia")
pprint(dataset["train"][0])
```

### Evaluation

```python
from datasets import load_dataset
import evaluate

dataset = load_dataset("expansio/qa-wikipedia")
squad_v2 = evaluate.load("squad_v2")

predictions = [
    {"id": str(i), "prediction_text": "", "no_answer_probability": 1.0}
    for i, _ in enumerate(dataset["validation"])
]
references = [
    {"id": str(i), "answers": ex["answers"] or {"answer_start": [], "text": []}}
    for i, ex in enumerate(dataset["validation"])
]

print(squad_v2.compute(predictions=predictions, references=references))
```
