# QA-KPWr

**Hugging Face Repository**: [expansio/qa-kpwr](https://huggingface.co/datasets/expansio/qa-kpwr)

## Description

QA-KPWr is a Polish extractive question answering dataset built on passages from the Polish Corpus of Wrocław University of Technology (*Korpus Języka Polskiego Politechniki Wrocławskiej*, KPWr). KPWr is a manually annotated, multi-domain Polish corpus widely used for tasks such as named entity recognition and chunking, which makes QA-KPWr a natural complement to the existing CLARIN-PL KPWr benchmarks. Each example pairs a Polish question with a KPWr passage, follows a SQuAD 2.0-style format with optional answer spans, and is flagged for paraphrase and impossible-to-answer status.

## Tasks (input, output and metrics)

Extractive question answering with unanswerable questions.

**Input** (`question` + `context` columns): a Polish question and a passage drawn from KPWr.

**Output**: a character-level span inside `context`, or an abstention when no answer is present.

**Measurements**: SQuAD 2.0 metrics - `exact`, `f1`, `HasAns_exact`, `HasAns_f1`, `NoAns_f1`.

**Example**:

Question: `Podczas jakiego procesu woda rozpada się na dwa elektrony, dwa kationy wodoru oraz cząsteczkę tlenu?`

Context (excerpt): `Fotoliza wody – rozpad wody pod wpływem światła...`

Answer: `Fotoliza wody`

## Data splits

| Subset     | Cardinality (questions) |
|------------|------------------------:|
| train      |                   7,563 |
| validation |                   1,878 |
| test       |                       0 |

## Schema

| Column          | Type                                                 | Description                                                            |
|-----------------|------------------------------------------------------|------------------------------------------------------------------------|
| `question`      | string                                               | Question text in Polish                                                |
| `context`       | string                                               | KPWr passage                                                           |
| `answers`       | {`answer_start`: int[], `answer_end`: int[], `text`: string[]} | Answer spans; `null` when `is_impossible` is true            |
| `is_impossible` | bool                                                 | `true` if the question cannot be answered from `context`               |
| `is_paraphrase` | bool                                                 | `true` if the question is a paraphrase of another item on this context |
| `dataset`       | string                                               | Source identifier (`KPWR`)                                             |
| `context_id`    | int64                                                | Shared id of all questions for the same context                        |

## License

TBD - source passages from KPWr (originally CC BY 3.0).

## Links

[HuggingFace](https://huggingface.co/datasets/expansio/qa-kpwr)

[KPWr (CLARIN-PL)](https://clarin-pl.eu/index.php/kpwr-en/)

[Expansio Software House](https://expans.io)

[CLARIN-PL](https://clarin-pl.eu/)

## Examples

### Loading

```python
from pprint import pprint
from datasets import load_dataset

dataset = load_dataset("expansio/qa-kpwr")
pprint(dataset["train"][0])
```
