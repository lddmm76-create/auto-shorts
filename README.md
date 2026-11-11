# Auto Shorts — Korean Beauty Video Automation

이 저장소는 한국어 뷰티·헬스 숏폼 제작을 위한 개인용 Agent Skill입니다.

## 적용 대상
- TikTok / Instagram Reels / YouTube Shorts용 세로 영상
- 한국어 내레이션 및 영문+한글 2줄 자막
- AI 모델/B-roll 장면을 장면별로 구성
- FFmpeg로 컷 편집, 세로 비율 변환, 자막 삽입, 음량 정규화
- 검수 후 MP4 및 SRT 전달

## 설치

저장소 루트에서 아래 명령으로 Skill을 지원하는 에이전트에 추가합니다.

    npx skills add lddmm76-create/auto-shorts

에이전트가 설치 위치를 묻는 경우 현재 사용하는 도구(Claude Code / Codex 등)를 선택합니다.

## Windows 사전 준비

1. FFmpeg 설치: winget install Gyan.FFmpeg
2. 새 PowerShell 창에서 확인:
       ffmpeg -version
       ffprobe -version
3. 한국어 폰트는 Noto Sans KR 또는 Noto Sans CJK KR 사용을 권장합니다.
4. NVIDIA CUDA는 필요하지 않습니다. Intel Iris Xe 환경에서는 CPU 호환 렌더링을 사용합니다.

## 중요한 선택

- AI 영상 생성은 연결된 생성 도구 및 해당 도구의 무료/유료 사용 조건에 따릅니다. 유료 크레딧은 사전 승인 없이 사용하지 않습니다.
- FFmpeg 편집·합성은 로컬에서 실행합니다.
- Remotion Shorts 원본 템플릿은 한국어 글꼴을 기본 지원하지 않으므로 그대로 한국어 영상에 사용하지 않습니다. 상업용 자동 렌더링 전에 Remotion 라이선스도 확인합니다.
- 게시 전 반드시 영상과 자막을 검수하고 사용자 승인을 받습니다.

## Skill

실제 작업 지침: .agents/skills/beauty-short-video/SKILL.md
