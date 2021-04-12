## 도구 설정

#### Mypy를 사용한 타입 헌팅
mypy는 파이썬에서 가장 일반적으로 사용하는 정적 타입 검사도구이다.

프로젝트의 모든 파일을 분석하여 타입 불일치를 검사하는데 유용하다.

[다운로드]
pip install mypy

[사용법]
mypy 파일명

가끔 잘못된 탐지를 하는 경우도 있기 때문에 문장 끝에 주석을 추가하여 무시할 수 도 있다.
```python
type_to_ignore = "somefthing" # type: ignore
```

#### Pylint를 사용한 코드 검사
PEP-8 코드의 구조를 검사하는 것중 pycodestyle, Flake8같은 것이 있는데, 가장 완결성이 높고 엄격하고 설정 가능한 옵션이 많은 도구로 Pylint를 추천한다.

[다운로드]
pip install pylint

[사용법]
pylint

.pylintrc 파일을 통해 설정 값을 바꿀 수 있다.

#### 자동 검사 설정
리눅스 개발환경에서 빌드 자동화는 **makefile**을 사용하는 것이다. 빌드 외에도 포매팅 검사나 코딩 컨벤션 검사를 자동화하기 위해 사용할 수 있다.

[예시]
```bash
typehint:
mypy  src/  tests/

test:
pytest  tests/

lint:
pylint  src/  tests/

checklist: lint typehint  test

.PHONY: typehint test lint checklist
```
`Makefile에서는 명령어가 있는 행에서는 공백이 아닌 탭으로 들여쓰기 해야 한다.`

이후 커맨드 `make checklist`입력하면 된다. 이것은 다음과 같은 단계를 가진다.
1. 코딩 가이드라인 검사
2. 올바른 타입을 사용했는지 검사
3. 최종적으로 테스트 실행
