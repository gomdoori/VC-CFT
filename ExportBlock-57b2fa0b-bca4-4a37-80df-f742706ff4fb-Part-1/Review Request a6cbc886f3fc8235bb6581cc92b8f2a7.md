# Review Request

이 검토는 **CSV 입력 작업 없이**, `Gesture_Country Pairs.md` 파일만 보고
candidate 내용에 문제가 있는지 확인하는 용도입니다.

## 왜 이 검토를 하나

기존 Table 5 / RQ2는 대체로

- `Can I use this gesture in {country} with the intended meaning "{meaning}"?`

처럼 yes/no appropriateness를 묻는 구조였습니다.

그런데 여기서 모델이 `No`라고 답했다고 해서,
그 모델이 정말 그 나라의 local meaning이나 local harm을 알고 `No`한 것인지는 바로 알 수 없습니다.
그냥 보수적으로 `No`했을 수도 있고, 불확실해서 그렇게 답했을 수도 있습니다.

그래서 이번 검토에서는 각 `(gesture, country)` pair에 대해,
우리가 정리한 `Candidate`가 실제 `Raw Evidence`를 과장 없이 잘 대표하는지 먼저 확인하려고 합니다.

즉 이 검토는:

- candidate 문장이 raw evidence와 맞는지
- candidate gold type이 과하지 않은지
- mixed evidence를 너무 단정적으로 요약하지 않았는지

를 점검하는 단계입니다.

## Gold Type 기준

이번 검토에서는 아래 기준으로 `candidate_gold_type`을 보고 있습니다.

### `local_meaning`

아래에 가까우면 `local_meaning`으로 봅니다.

- raw evidence가 **대체로 한 방향의 local interpretation**으로 모인다
- minor noise가 있더라도, **하나의 대표 의미**로 요약해도 무리가 없다
- reviewer가 보기에 `but`, `or`, `depends on` 같은 단서를 굳이 붙이지 않아도 candidate를 설명할 수 있다

쉽게 말해:

- “이 지역에서 이 제스처는 보통 이렇게 읽힌다”

라고 말해도 과장이 아닌 경우입니다.

### `context_dependent`

아래에 가까우면 `context_dependent`로 봅니다.

- 반복적으로 보이는 의미는 있지만, **맥락/세대/orientation/사용 상황에 따라 달라진다**
- offensive reading과 benign reading이 함께 보이거나,
같은 offensive 계열이라도 해석이 단일 의미로 고정되기 어렵다
- 하나의 local meaning으로 정리할 수는 있어도, 그대로 못 박으면 과장될 위험이 있다

쉽게 말해:

- “이런 의미로 자주 읽히긴 하는데, 상황 따라 다르다”

에 가까운 경우입니다.

### `no_clear_shared_meaning`

아래에 가까우면 `no_clear_shared_meaning`으로 봅니다.

- raw evidence가 **너무 제각각**이어서 shared canonical meaning을 세우기 어렵다
- `Unsure`, `I don't know`, `no meaning`, 상충되는 해석이 많이 섞여 있다
- 억지로 한 줄 meaning을 만들면 raw evidence를 과도하게 일반화하게 된다

쉽게 말해:

- “이 pair는 지금 evidence만으로는 하나의 shared local meaning을 세우기 어렵다”

인 경우입니다.

## Gold Type 판단 팁

- candidate 문장에 `or / but / depending on`이 꼭 필요해 보이면 `context_dependent` 가능성이 큽니다.
- raw evidence를 읽었을 때 reviewer 본인도 “대표 의미 하나를 못 정하겠다”는 느낌이면 `no_clear_shared_meaning` 쪽이 더 안전합니다.
- 아주 깔끔해 보여도, 실제 raw evidence가 mixed면 `local_meaning`으로 올리지 않는 쪽이 더 보수적입니다.

## 부탁드리는 것

각 md 파일에서 아래 두 부분만 집중해서 봐주시면 됩니다.

- `Candidate`
- `Raw Evidence`

`Quick Summary`는 맥락 참고용입니다.

## 무엇을 확인하면 되나

아래 질문에 답해주시면 충분합니다.

1. `Candidate local meaning`이 `Raw Evidence`와 내용적으로 맞는가?
2. `Candidate gold type`이 과하지 않은가?
    - `local_meaning`
    - `context_dependent`
    - `no_clear_shared_meaning`
3. candidate가 raw evidence보다 더 강하게 일반화하거나 과장하고 있지는 않은가?
4. mixed evidence인데 너무 단정적으로 적혀 있지는 않은가?

## 어떤 경우를 문제로 보면 되나

### `OK`

- candidate wording이 대체로 적절함
- raw evidence가 그 candidate를 충분히 지지함

### `수정 필요`

- 방향은 맞지만 문구가 너무 강함 / 너무 좁음 / 너무 넓음
- `local_meaning`보다 `context_dependent`가 더 안전해 보임
- wording만 조금 다듬으면 될 것 같음

### `문제 있음`

- candidate가 raw evidence와 잘 안 맞음
- evidence가 제각각인데 하나의 stable meaning으로 몰아감
- `no_clear_shared_meaning` 또는 `context_dependent`로 내려야 할 것 같음
- candidate가 raw evidence에 없는 내용을 끌어옴

## 답변은 어떻게 주면 되나

각 md 파일 맨 아래에 있는 `Reviewer Response Template`를 그대로 복사해서
Comments란에 답해주시면 됩니다.

필드 뜻이 헷갈리면 아래를 참고하시면 됩니다.

- `candidate_local_meaning_ok`
    - 위의 [무엇을 확인하면 되나](https://www.notion.so/Review-Request-a6cbc886f3fc8235bb6581cc92b8f2a7?pvs=21) 1번 참고
- `candidate_gold_type_ok`
    - 위의 [Gold Type 기준](https://www.notion.so/Review-Request-a6cbc886f3fc8235bb6581cc92b8f2a7?pvs=21) 참고
- `supporting_raw_evidence`
    - 실제로 근거가 된 `Raw Evidence` bullet을 짧게 적어주시면 됩니다
    - 가능하면 `instance_id + 짧은 excerpt` 형태가 좋습니다

형식은 아래처럼 되어 있습니다.

```
candidate_local_meaning_ok: yes / no
candidate_gold_type_ok: yes / no
status: OK / 수정 필요 / 문제 있음
supporting_raw_evidence:
ai_used: yes / no
ai_help_for: translation / summarization / wording / none
comment:
suggestion:
```

여기서 `suggestion`은 선택입니다.
`supporting_raw_evidence`는 가능하면 꼭 적어주세요.

예시를 먼저 보고 싶으면:

- `MD_ONLY_REVIEW_EXAMPLE__Fingers_Crossed__Vietnam.md`
    
    [MD_ONLY_REVIEW_EXAMPLE__Fingers_Crossed__Vietnam](https://www.notion.so/MD_ONLY_REVIEW_EXAMPLE__Fingers_Crossed__Vietnam-66dbc886f3fc831eb4e001cd5e709f4d?pvs=21)
    

## AI를 사용해도 직접 확인해야 하는 부분

AI를 사용해서 번역, 요약, wording 정리를 하는 것은 괜찮습니다.
하지만 아래는 reviewer가 **직접** 확인해주셔야 합니다.

- `Candidate local meaning`이 실제 `Raw Evidence`와 내용적으로 맞는지
- `Candidate gold type`이 과하지 않은지
- mixed evidence를 하나의 stable meaning으로 과도하게 일반화하지 않았는지
- `supporting_raw_evidence`로 실제 근거를 짚을 수 있는지

즉 AI는 보조 도구일 수 있지만,
최종 판단은 reviewer 본인이 `Raw Evidence`를 직접 읽고 내려주시면 됩니다.

## 핵심만 한 줄로

이 검토는 **candidate가 보기 좋게 써졌는지**가 아니라,
**candidate가 raw evidence를 과장 없이 대표하는지**를 봐주시면 됩니다.

---

[Gesture_Country Pairs](Review%20Request/Gesture_Country%20Pairs%201b9bc886f3fc82a7860581ae3196bc10.csv)