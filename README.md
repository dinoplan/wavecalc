# WaveCalc

**Waveform Calculator** — 브라우저에서 동작하는 파형 계산기입니다. 설치나 서버 없이 `index.html` 하나로 동작하며, 불러온 데이터는 브라우저 밖으로 나가지 않습니다.

- 사이트: https://dinoplan.github.io/wavecalc/
- 현재 버전: **rev.1.0.0** (2026-10-14)

## 기능
- CSV / Excel(xlsx, xls) 파형 불러오기 — 열 하나 = 채널 하나, 헤더 없음
- 시간 파형(INDEX / TIME), FFT 스펙트럼(Freq. / Harm. 로그축)
- Signal / Noise floor / SNR / ENOB (MATLAB `FFT_SNR`, `FFT_NOISE` 방식)
- Measure: RMS, AC RMS, MAX, MIN, PK-PK, MEAN / n차 크기·위상, THD …
- Math Calc.: `MATH1 = (CH1 - CH2) - meas(time,rms,CH1)`, `abs sqrt ln log10 exp delay`
- `delay(x, 값[, deg|min|samp|us])` — 음수 = 지연, 양수 = 앞섬 (FFT 위상 회전 + sinc 보간)
- Save / Load: 세팅(.json) + 데이터(.csv)

## 버전 규칙
`rev.주.부.수정` (예: rev.1.2.3)
- **주**: 세팅 파일 형식이 바뀌어 예전 파일과 호환이 깨질 때
- **부**: 기능 추가
- **수정**: 버그 수정, 화면 다듬기

## 변경 이력
### rev.1.0.0 — 2026-10-14
- 첫 공개 버전

## 사용 라이브러리 (CDN)
- Plotly.js 2.27.0, SheetJS (xlsx) 0.18.5 — cdnjs.cloudflare.com
