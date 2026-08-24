# SceneVoice

AI 기반 배리어프리 영상 화면해설 자동 생성 도구

영상의 대사 공백 구간을 찾아 장면을 분석하고, 화면해설 대본과
TTS 내레이션을 자동으로 생성해 삽입한다.

## 배경

시각장애인과 고령층의 미디어 접근성을 위한 화면해설 콘텐츠는
수요가 늘고 있으나, 제작에 많은 비용과 인력이 소요된다.
학교, 지자체, 공공기관이 화면해설 콘텐츠를 손쉽게 제작할 수 있도록
하는 것을 목표로 한다.

## 처리 흐름

1. 영상에서 오디오 추출 (FFmpeg)
2. 음성 인식으로 대사 구간 추출 (Whisper)
3. 대사가 없는 구간 계산
4. 해당 구간의 프레임 추출 후 장면 분석 (Vision API)
5. 구간 길이에 맞는 해설 문장 생성
6. TTS 음성 생성 및 원본 영상에 믹싱
7. 편집기에서 검수 후 최종 출력

## 기술 스택

- 백엔드: Java, Spring Boot
- AI 워커: Python, Whisper, MLX
- 미디어 처리: FFmpeg
- 연결: 메시지 큐 기반 비동기 처리

## 설계 원칙

- 최종 배포 전 사람의 검수를 거치는 구조 (Human-in-the-Loop)
- 음성 인식은 로컬 추론으로 처리하여 원가 절감 및 콘텐츠 외부 유출 방지

## 진행 상황

- [x] 개발 환경 구성
- [x] MLX 로컬 추론 성능 비교 ([결과](docs/benchmark.md))
- [ ] 무음 구간 검출
- [ ] 장면 분석 및 해설 생성
- [ ] TTS 생성 및 믹싱
- [ ] Spring Boot 백엔드
- [ ] 검수 편집기

## 문서

- [Whisper 추론 성능 벤치마크](docs/benchmark.md)

## 실행 환경 준비

    brew install ffmpeg
    python3 -m venv venv
    source venv/bin/activate
    pip install -r requirements.txt
