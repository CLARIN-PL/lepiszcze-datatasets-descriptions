# QA-NKJP

**Hugging Face Repository**: [expansio/qa-nkjp](https://huggingface.co/datasets/expansio/qa-nkjp)

## Description

QA-NKJP is a Polish extractive question answering dataset built on passages from the National Corpus of Polish (*Narodowy Korpus Języka Polskiego*, NKJP). NKJP brings together mixed-genre Polish texts from press, fiction, transcribed speech and web sources, which makes QA-NKJP a domain-diverse counterpart to QA-Wikipedia. Each example pairs a Polish question with a context paragraph, follows a SQuAD 2.0-style format with optional answer spans, and is flagged for paraphrase and impossible-to-answer status.

## Tasks (input, output and metrics)

Extractive question answering with unanswerable questions.

**Input** (`question` + `context` columns): a Polish question and a passage drawn from NKJP.

**Output**: a character-level span inside `context`, or an abstention when no answer is present.

**Measurements**: SQuAD 2.0 metrics - `exact`, `f1`, `HasAns_exact`, `HasAns_f1`, `NoAns_f1`.

**Example**:

Question: `W którym roku Irena Santor zdobyła jako pierwsza nagrodę w Operze Leśnej?`

Context (excerpt): `...laureatka pierwszego festiwalu piosenki w 1961 r. Irena Santor...`

Answer: `w 1961`

## Data splits

| Subset     | Cardinality (questions) |
|------------|------------------------:|
| train      |                   4,417 |
| validation |                     908 |
| test       |                       0 |

## Schema

| Column          | Type                                                 | Description                                                            |
|-----------------|------------------------------------------------------|------------------------------------------------------------------------|
| `question`      | string                                               | Question text in Polish                                                |
| `context`       | string                                               | NKJP passage                                                           |
| `answers`       | {`answer_start`: int[], `answer_end`: int[], `text`: string[]} | Answer spans; `null` when `is_impossible` is true            |
| `is_impossible` | bool                                                 | `true` if the question cannot be answered from `context`               |
| `is_paraphrase` | bool                                                 | `true` if the question is a paraphrase of another item on this context |
| `dataset`       | string                                               | Source identifier (`NKJP`)                                             |
| `context_id`    | int64                                                | Shared id of all questions for the same context                        |

## License

TBD - source passages from NKJP, see [nkjp.pl](http://nkjp.pl/) for upstream terms.

## Links

[HuggingFace](https://huggingface.co/datasets/expansio/qa-nkjp)

[NKJP](http://nkjp.pl/)

[Expansio Software House](https://expans.io)

[CLARIN-PL](https://clarin-pl.eu/)

## Examples

### Loading

```python
from pprint import pprint
from datasets import load_dataset

dataset = load_dataset("expansio/qa-nkjp")
pprint(dataset["train"][0])
```
