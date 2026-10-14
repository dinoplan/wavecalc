# WaveCalc

**Waveform Calculator** — 브라우저에서 동작하는 파형 계산기입니다. 설치나 서버 없이 `index.html` 하나로 동작하며, 불러온 데이터는 브라우저 밖으로 나가지 않습니다.

- 사이트: https://dinoplan.github.io/wavecalc/
- 사용 설명서: https://dinoplan.github.io/wavecalc/manual.html (앱 머리줄 **Manual** 버튼)
- 현재 버전: **rev.1.4.3** (2026-10-14)

## 기능
- CSV / Excel(xlsx, xls) 파형 불러오기 — 열 하나 = 채널 하나. 앞쪽 설명·헤더 줄 자동 건너뜀(헤더는 Legend로), NaN·N/A·Inf 등은 빈칸 처리
- 데이터 신뢰성 표시: 제목 앞 ●(양호/주의/확인 필요), 눌러서 파일·채널별 이유 확인
- 시간 파형(INDEX / TIME), FFT 스펙트럼(Freq. / Harm. 로그축)
- Signal / Noise floor / SNR / ENOB (MATLAB `FFT_SNR`, `FFT_NOISE` 방식)
- Measure: RMS, AC RMS, MAX, MIN, PK-PK, MEAN / n차 크기·위상, THD …
- Math Calc.: `MATH1 = (CH1 - CH2) - meas(time,rms,CH1)`, `abs sqrt ln log10 exp delay`
- `delay(x, 값[, 단위])` — 각도(기본, °): −60 = 60° 지연 (위상 관례) / 시간(s, ms, us, ns, ps): +10 ms = 10 ms 지연 (시간 관례). FFT 위상 회전 + sinc 보간
- Math Graph: `meas(time, rms, CH1~10, [10,20,…,100])` → x=지정값, y=계측값 그래프 (오른쪽 패널 ▾ 전환)
- Save / Load: 세팅(.json) + 데이터(.csv)

## 저장소 파일
- `index.html` — 앱
- `manual.html` — 사용 설명서 (index.html과 같은 폴더에 둘 것)
- `README.md` — 이 문서

## 버전 규칙
`rev.주.부.수정` (예: rev.1.2.3)
- **주**: 세팅 파일 형식이 바뀌어 예전 파일과 호환이 깨질 때
- **부**: 기능 추가
- **수정**: 버그 수정, 화면 다듬기

## 변경 이력
### rev.1.4.3 — 2026-10-14
- 사용 설명서 `manual.html` 추가, 머리줄 Load 옆 **Manual** 버튼으로 새 탭에서 열기 (GitHub Pages에서는 같은 폴더 파일, 그 밖에서는 GitHub Pages 주소)

### rev.1.4.2 — 2026-10-14
- 입력 채널 표에 Math Graph(XY) 결과 행 표시 (XY 표시, 오른쪽이 Frequency일 때도 보임). 체크 = Math Graph 보이기, Legend 편집 → Math Graph 범례에 반영. 샘플 수 칸은 점 수, 나머지는 –
- GROUP 행에 Legend 편집 추가 (Measure 그룹 상자 제목에 표시). 샘플 수·FFT 사용은 멤버 값(다르면 범위), Noise 기준은 멤버 일괄 변경(다르면 "혼합"), dB 칸은 –
- 세팅 파일에 그룹 Legend, XY Legend 저장

### rev.1.4.1 — 2026-10-14
- 입력 채널 표 아래에 GROUP 행 표시 (정보 칸 없이 이름 + 체크). 체크로 묶인 채널 파형을 한꺼번에 보이기/숨기기, 일부만 켜져 있으면 – 표시

### rev.1.4.0 — 2026-10-14
- **Group Setting** (Math Calc. 옆): `GROUP1 = CH1, CH2, CH3` 또는 `CH1~CH5, CH7` 처럼 채널 묶음 정의 (MATH 채널도 가능)
- `meas(time, rms, GROUP1)` / `meas(time, rms, GROUP1, [x값])` → Math Graph (점마다 채널 이름 표시)
- 파형 수식에 그룹 사용: `GROUP1 * 2`, `delay(GROUP1, -60)`, `GROUP1 - CH8` → 채널마다 계산해 MATH1_1, MATH1_2 … 여러 파형. Legend는 각 채널의 Legend
- 여러 파형이 된 MATH1 은 그 자체로 그룹처럼 다시 쓸 수 있음 (`meas(time, max, MATH1)`)
- Measure 채널 목록에 GROUP 추가. 고르면 채널별 값을 점선 상자 안에 칸으로 나눠 표시
- 세팅 파일(.json)에 groups 저장

### rev.1.3.2 — 2026-10-14
- CSV 인코딩 자동 판단: BOM(UTF-8 / UTF-16) → UTF-8 → 안 맞으면 CP949(엑셀 "CSV(쉼표로 분리)"). 한글 헤더가 깨지지 않음. UTF-8이 아니면 상태줄에 인코딩 표시

### rev.1.3.1 — 2026-10-14
- 확장자 대신 파일 앞 바이트로 형식 판단: 이름이 .csv여도 실제 엑셀(xlsx/xls)이면 엑셀로 읽음
- 엑셀 파일은 50MB까지 (압축을 풀면 수 배로 커짐). 넘으면 "CSV UTF-8로 저장해서 넣어 주세요" 팝업

### rev.1.3.0 — 2026-10-14
- Save CSV 첫 행에 채널 헤더(`CH1,CH2,…`)를 넣음. 다시 불러오면 헤더를 자동으로 건너뛰고 Legend 기본값으로 사용
- 200MB를 넘는 데이터 파일은 읽지 않고 안내 팝업을 띄움 (확인 / × / Esc / 바깥 클릭으로 닫기)

### rev.1.2.4 — 2026-10-14
- delay 시간 단위의 부호를 시간 관례로 변경: `delay(CH1, 10, ms)` = 10 ms 지연. 각도는 그대로(−60° = 지연)

### rev.1.2.3 — 2026-10-14
- delay 시간 지연 단위 추가: `delay(CH1, -10, us)` (s, ms, us, ns, ps). 단위 생략 시 각도(°)

### rev.1.2.2 — 2026-10-14
- delay 단위 옵션(min, samp, us) 제거: `delay(파형, 각도[°])` 두 칸만 사용

### rev.1.2.1 — 2026-10-14
- 데이터 신뢰성 기준을 개수 기준으로 변경 (빡빡하게)
  - 주의: 헤더 10줄 초과, 이상한 값(NaN·Inf·N/A·중간 빈칸 등) 1개 이상, 클리핑 의심 1개 이상
  - 확인 필요: 헤더 20줄 초과, 이상한 값 5개 이상, 클리핑 의심 5개 이상
- 헤더 줄은 모든 채널에 이름이 있을 때만 Legend로 사용

### rev.1.2.0 — 2026-10-14
- 데이터 시작 자동 판정: 숫자 줄이 5줄 이상 연속되는 첫 줄부터 데이터, 앞쪽 설명·헤더와 뒤쪽 꼬리 줄 무시
- 데이터 바로 위 헤더 줄을 Legend 기본값으로 사용
- 빈 값 표기(NaN, NA, N/A, #N/A, null, -, --, 엑셀 오류값)와 Inf를 빈칸으로 처리
- "데이터 시작 행" 수동 지정 칸 (자동으로 되돌리기 가능)
- 데이터 신뢰성 ●: 제목 앞 전체 표시 + 채널별 표시, 눌러서 이유 보기 (FFT 구간 빈 값, 짧은 채널, 클리핑 의심, 샘플·주기 부족, 무신호 등)

### rev.1.1.0 — 2026-10-14
- Math Graph 추가: 오른쪽 패널 제목 ▾ 에서 Frequency domain ↔ Math Graph 전환
- `meas(영역, 항목, 채널범위|[채널목록], [차수], [x값])` 로 XY 그래프용 MATH 생성 (x 생략 시 1,2,3…)
- Math Graph: Auto / 수동 축, MATH별 체크박스로 겹쳐 보기, 범례 클릭으로 숨기기
- XY MATH끼리, XY와 숫자 사이 사칙연산 지원 (예: `MATH1 * 2`)
- 범례 클릭 숨김을 그래프별로 따로 동작하도록 되돌림 (Time / Freq / Math Graph 각각)

### rev.1.0.1 — 2026-10-14
- 드래그 칸과 "파일을 업로드하세요"에서도 세팅 파일(.json)을 불러올 수 있게 함 (세팅+데이터 2개 동시 가능)

### rev.1.0.0 — 2026-10-14
- 첫 공개 버전

## 사용 라이브러리 (CDN)
- Plotly.js 2.27.0, SheetJS (xlsx) 0.18.5 — cdnjs.cloudflare.com
