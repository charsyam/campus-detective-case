# 사건 조사 보고서

## 1. 현재 위치
/c/campus-detective-case/campus-detective-case

## 2. 사건 자료 목록
total 26
drwxr-xr-x 1 pc 197121    0 May 22 15:25 ./
drwxr-xr-x 1 pc 197121    0 May 22 14:10 ../
drwxr-xr-x 1 pc 197121    0 May 22 14:26 .git/
drwxr-xr-x 1 pc 197121    0 May 22 14:10 .github/
-rw-r--r-- 1 pc 197121 1252 May 22 14:10 README.md
drwxr-xr-x 1 pc 197121    0 May 22 14:10 case/
-rw-r--r-- 1 pc 197121 3828 May 22 14:10 case-report-sample.md
-rw-r--r-- 1 pc 197121  120 May 22 15:37 case-report.md
-rwxr-xr-x 1 pc 197121 7637 May 22 14:10 check_report.py*
drwxr-xr-x 1 pc 197121    0 May 22 14:10 docs/
drwxr-xr-x 1 pc 197121    0 May 22 14:10 evidence/
-rw-r--r-- 1 pc 197121    4 May 22 15:25 memo.txt
drwxr-xr-x 1 pc 197121    0 May 22 14:10 project/
drwxr-xr-x 1 pc 197121    0 May 22 14:59 workspace/

## 2-1. 폴더별 자료 목록
### case
briefing.md
suspects.md
timeline.md
### evidence
access.log
chat.log
file-events.log
### project
draft_report.md
final_report.md
src/

## 3. 사건 개요
# 사건 개요

캠퍼스 해커톤 마감 10분 전, Team Nova의 `final_report.md`가 제출 폴더에서 사라졌습니다.

운영진은 서버 로그와 팀 채팅 기록을 복구했습니다.

조사 목표:

- `final_report.md`가 언제 사라졌는지 찾기
- 파일 상태 변화와 가까운 사용자 이름 찾기
- 아직 확실하지 않은 점을 보고서에 남기기

주의:

이 실습은 명령어 연습을 위한 가벼운 시나리오입니다.
결론은 로그에 남은 근거를 바탕으로 조심스럽게 작성합니다.

## 4. 로그 증거
evidence/access.log:12:2026-05-20 08:46:10 INFO GET /project/final_report.md 404 user=jimin
evidence/access.log:18:2026-05-20 08:49:53 INFO GET /project/final_report.md 404 user=sora
evidence/access.log:21:2026-05-20 08:51:02 INFO POST /upload 201 user=sora file=final_report.md
evidence/access.log:22:2026-05-20 08:51:22 INFO GET /project/final_report.md 200 user=sora
evidence/access.log:23:2026-05-20 08:52:03 INFO GET /project/final_report.md 200 user=jimin
evidence/access.log:24:2026-05-20 08:52:41 INFO GET /project/final_report.md 200 user=minho
evidence/access.log:28:2026-05-20 08:55:05 INFO GET /project/final_report.md 200 user=sora
evidence/access.log:30:2026-05-20 08:56:01 INFO POST /file/action 200 user=minho target=final_report.md result=removed
evidence/access.log:31:2026-05-20 08:56:18 INFO GET /project/final_report.md 404 user=sora
evidence/access.log:32:2026-05-20 08:57:02 INFO GET /project/final_report.md 404 user=jimin
evidence/access.log:35:2026-05-20 08:58:25 INFO GET /project/final_report.md 404 user=sora
evidence/chat.log:6:2026-05-20 08:45 minho: 파일 이름 규칙이 final_report.md 맞지?
evidence/chat.log:7:2026-05-20 08:46 jimin: 응. 마지막 파일은 final_report.md.
evidence/chat.log:8:2026-05-20 08:47 sora: 아직 final_report 없어서 내가 올릴게.
evidence/chat.log:9:2026-05-20 08:50 sora: final_report.md 업로드 준비 중.
evidence/chat.log:10:2026-05-20 08:51 sora: final_report.md 올렸어.
evidence/chat.log:15:2026-05-20 08:56 sora: 잠깐, final_report가 안 보여.
evidence/file-events.log:14:2026-05-20 08:51:02 UPLOAD project/final_report.md user=sora
evidence/file-events.log:15:2026-05-20 08:51:20 CHECK project/final_report.md user=system
evidence/file-events.log:16:2026-05-20 08:52:03 OPEN project/final_report.md user=jimin
evidence/file-events.log:17:2026-05-20 08:52:41 OPEN project/final_report.md user=minho
evidence/file-events.log:18:2026-05-20 08:53:11 COPY project/final_report.md project/final_report_backup.md user=system
evidence/file-events.log:21:2026-05-20 08:55:03 OPEN project/final_report.md user=sora
evidence/file-events.log:23:2026-05-20 08:55:50 RENAME project/final-report.md project/final_report.md user=minho status=failed
evidence/file-events.log:24:2026-05-20 08:56:01 FILE_EVENT target=project/final_report.md user=minho action=cleanup result=removed
evidence/file-events.log:25:2026-05-20 08:56:18 CHECK project/final_report.md user=sora status=missing
evidence/file-events.log:26:2026-05-20 08:57:02 CHECK project/final_report.md user=jimin status=missing
evidence/file-events.log:28:2026-05-20 08:58:03 CHECK submit/status user=sora status=missing_final_report
evidence/file-events.log:29:2026-05-20 08:58:20 RESTORE project/final_report.md user=admin source=backup
evidence/file-events.log:25:2026-05-20 08:56:18 CHECK project/final_report.md user=sora status=missing
evidence/file-events.log:26:2026-05-20 08:57:02 CHECK project/final_report.md user=jimin status=missing
evidence/file-events.log:28:2026-05-20 08:58:03 CHECK submit/status user=sora status=missing_final_report
evidence/access.log:30:2026-05-20 08:56:01 INFO POST /file/action 200 user=minho target=final_report.md result=removed
evidence/file-events.log:24:2026-05-20 08:56:01 FILE_EVENT target=project/final_report.md user=minho action=cleanup result=removed

## 5. 용의자별 단서
./case/suspects.md:3:## jimin
./case-report-sample.md:74:evidence/file-events.log:26:2026-05-20 08:57:02 CHECK project/final_report.md user=jimin status=missing
./case-report-sample.md:83:grep -rn "jimin" .
./case-report-sample.md:159:  23 user=jimin
./evidence/access.log:1:2026-05-20 08:40:01 INFO login user=jimin ip=10.0.0.11
./evidence/access.log:2:2026-05-20 08:40:09 INFO GET /project 200 user=jimin
./evidence/access.log:7:2026-05-20 08:43:01 INFO GET /project/draft_report.md 200 user=jimin
./evidence/access.log:10:2026-05-20 08:44:58 INFO GET /project/draft_report.md 200 user=jimin
./evidence/access.log:12:2026-05-20 08:46:10 INFO GET /project/final_report.md 404 user=jimin
./evidence/access.log:13:2026-05-20 08:46:44 INFO GET /project/draft_report.md 200 user=jimin
./evidence/access.log:14:2026-05-20 08:47:18 INFO POST /save 200 user=jimin file=draft_report.md
./evidence/access.log:17:2026-05-20 08:49:11 INFO GET /project/draft_report.md 200 user=jimin
./evidence/access.log:23:2026-05-20 08:52:03 INFO GET /project/final_report.md 200 user=jimin
./evidence/access.log:26:2026-05-20 08:54:06 INFO GET /project/draft_report.md 200 user=jimin
./evidence/access.log:27:2026-05-20 08:54:39 INFO POST /save 200 user=jimin file=draft_report.md
./evidence/access.log:32:2026-05-20 08:57:02 INFO GET /project/final_report.md 404 user=jimin
./evidence/access.log:36:2026-05-20 08:59:10 INFO GET /project/draft_report.md 200 user=jimin
./evidence/chat.log:1:2026-05-20 08:40 jimin: 발표 순서 확인했어.
./evidence/chat.log:4:2026-05-20 08:43 jimin: draft_report.md 문장 조금 고쳤어.
./evidence/chat.log:7:2026-05-20 08:46 jimin: 응. 마지막 파일은 final_report.md.
./evidence/chat.log:11:2026-05-20 08:52 jimin: 열어보니 내용 괜찮아.
./evidence/chat.log:13:2026-05-20 08:54 jimin: deadline 전에 draft는 남겨둬도 되나?
./evidence/chat.log:16:2026-05-20 08:57 jimin: 나도 404가 떠.
./evidence/file-events.log:2:2026-05-20 08:41:01 OPEN project/draft_report.md user=jimin
./evidence/file-events.log:5:2026-05-20 08:43:03 SAVE project/draft_report.md user=jimin
./evidence/file-events.log:9:2026-05-20 08:47:18 SAVE project/draft_report.md user=jimin
./evidence/file-events.log:10:2026-05-20 08:48:05 OPEN project/draft_report.md user=jimin
./evidence/file-events.log:11:2026-05-20 08:49:07 SAVE project/draft_report.md user=jimin
./evidence/file-events.log:16:2026-05-20 08:52:03 OPEN project/final_report.md user=jimin
./evidence/file-events.log:19:2026-05-20 08:54:06 OPEN project/draft_report.md user=jimin
./evidence/file-events.log:20:2026-05-20 08:54:39 SAVE project/draft_report.md user=jimin
./evidence/file-events.log:26:2026-05-20 08:57:02 CHECK project/final_report.md user=jimin status=missing
./evidence/file-events.log:30:2026-05-20 08:59:10 OPEN project/draft_report.md user=jimin
./workspace/evidence/access.log:1:2026-05-20 08:40:01 INFO login user=jimin ip=10.0.0.11
./workspace/evidence/access.log:2:2026-05-20 08:40:09 INFO GET /project 200 user=jimin
./workspace/evidence/access.log:7:2026-05-20 08:43:01 INFO GET /project/draft_report.md 200 user=jimin
./workspace/evidence/access.log:10:2026-05-20 08:44:58 INFO GET /project/draft_report.md 200 user=jimin
./workspace/evidence/access.log:12:2026-05-20 08:46:10 INFO GET /project/final_report.md 404 user=jimin
./workspace/evidence/access.log:13:2026-05-20 08:46:44 INFO GET /project/draft_report.md 200 user=jimin
./workspace/evidence/access.log:14:2026-05-20 08:47:18 INFO POST /save 200 user=jimin file=draft_report.md
./workspace/evidence/access.log:17:2026-05-20 08:49:11 INFO GET /project/draft_report.md 200 user=jimin
./workspace/evidence/access.log:23:2026-05-20 08:52:03 INFO GET /project/final_report.md 200 user=jimin
./workspace/evidence/access.log:26:2026-05-20 08:54:06 INFO GET /project/draft_report.md 200 user=jimin
./workspace/evidence/access.log:27:2026-05-20 08:54:39 INFO POST /save 200 user=jimin file=draft_report.md
./workspace/evidence/access.log:32:2026-05-20 08:57:02 INFO GET /project/final_report.md 404 user=jimin
./workspace/evidence/access.log:36:2026-05-20 08:59:10 INFO GET /project/draft_report.md 200 user=jimin
./workspace/evidence/chat.log:1:2026-05-20 08:40 jimin: 발표 순서 확인했어.
./workspace/evidence/chat.log:4:2026-05-20 08:43 jimin: draft_report.md 문장 조금 고쳤어.
./workspace/evidence/chat.log:7:2026-05-20 08:46 jimin: 응. 마지막 파일은 final_report.md.
./workspace/evidence/chat.log:11:2026-05-20 08:52 jimin: 열어보니 내용 괜찮아.
./workspace/evidence/chat.log:13:2026-05-20 08:54 jimin: deadline 전에 draft는 남겨둬도 되나?
./workspace/evidence/chat.log:16:2026-05-20 08:57 jimin: 나도 404가 떠.
./workspace/evidence/file-events.log:2:2026-05-20 08:41:01 OPEN project/draft_report.md user=jimin
./workspace/evidence/file-events.log:5:2026-05-20 08:43:03 SAVE project/draft_report.md user=jimin
./workspace/evidence/file-events.log:9:2026-05-20 08:47:18 SAVE project/draft_report.md user=jimin
./workspace/evidence/file-events.log:10:2026-05-20 08:48:05 OPEN project/draft_report.md user=jimin
./workspace/evidence/file-events.log:11:2026-05-20 08:49:07 SAVE project/draft_report.md user=jimin
./workspace/evidence/file-events.log:16:2026-05-20 08:52:03 OPEN project/final_report.md user=jimin
./workspace/evidence/file-events.log:19:2026-05-20 08:54:06 OPEN project/draft_report.md user=jimin
./workspace/evidence/file-events.log:20:2026-05-20 08:54:39 SAVE project/draft_report.md user=jimin
./workspace/evidence/file-events.log:26:2026-05-20 08:57:02 CHECK project/final_report.md user=jimin status=missing
./workspace/evidence/file-events.log:30:2026-05-20 08:59:10 OPEN project/draft_report.md user=jimin./case/suspects.md:8:## sora
./case-report-sample.md:71:evidence/file-events.log:14:2026-05-20 08:51:02 UPLOAD project/final_report.md user=sora
./case-report-sample.md:73:evidence/file-events.log:25:2026-05-20 08:56:18 CHECK project/final_report.md user=sora status=missing
./case-report-sample.md:84:grep -rn "sora" .
./case-report-sample.md:161:  20 user=sora
./evidence/access.log:3:2026-05-20 08:41:12 INFO login user=sora ip=10.0.0.12
./evidence/access.log:4:2026-05-20 08:41:20 INFO GET /project/assets 200 user=sora
./evidence/access.log:8:2026-05-20 08:43:27 INFO GET /project/screenshot.png 200 user=sora
./evidence/access.log:11:2026-05-20 08:45:31 INFO POST /upload 201 user=sora file=screen-main.png
./evidence/access.log:16:2026-05-20 08:48:45 INFO GET /project/assets 200 user=sora
./evidence/access.log:18:2026-05-20 08:49:53 INFO GET /project/final_report.md 404 user=sora
./evidence/access.log:19:2026-05-20 08:50:07 INFO POST /upload 201 user=sora file=team-photo.png
./evidence/access.log:21:2026-05-20 08:51:02 INFO POST /upload 201 user=sora file=final_report.md
./evidence/access.log:22:2026-05-20 08:51:22 INFO GET /project/final_report.md 200 user=sora
./evidence/access.log:28:2026-05-20 08:55:05 INFO GET /project/final_report.md 200 user=sora
./evidence/access.log:31:2026-05-20 08:56:18 INFO GET /project/final_report.md 404 user=sora
./evidence/access.log:34:2026-05-20 08:58:03 INFO GET /submit/status 200 user=sora
./evidence/access.log:35:2026-05-20 08:58:25 INFO GET /project/final_report.md 404 user=sora
./evidence/chat.log:2:2026-05-20 08:41 sora: 이미지 두 장만 더 올릴게.
./evidence/chat.log:5:2026-05-20 08:44 sora: 스크린샷 업로드 완료.
./evidence/chat.log:8:2026-05-20 08:47 sora: 아직 final_report 없어서 내가 올릴게.
./evidence/chat.log:9:2026-05-20 08:50 sora: final_report.md 업로드 준비 중.
./evidence/chat.log:10:2026-05-20 08:51 sora: final_report.md 올렸어.
./evidence/chat.log:15:2026-05-20 08:56 sora: 잠깐, final_report가 안 보여.
./evidence/chat.log:17:2026-05-20 08:58 sora: 제출 상태에 최종 보고서 누락이라고 나와.
./evidence/file-events.log:3:2026-05-20 08:41:30 OPEN project/assets/screen-main.png user=sora
./evidence/file-events.log:6:2026-05-20 08:44:12 UPLOAD project/assets/screen-main.png user=sora
./evidence/file-events.log:12:2026-05-20 08:50:07 UPLOAD project/assets/team-photo.png user=sora
./evidence/file-events.log:14:2026-05-20 08:51:02 UPLOAD project/final_report.md user=sora
./evidence/file-events.log:21:2026-05-20 08:55:03 OPEN project/final_report.md user=sora
./evidence/file-events.log:25:2026-05-20 08:56:18 CHECK project/final_report.md user=sora status=missing
./evidence/file-events.log:28:2026-05-20 08:58:03 CHECK submit/status user=sora status=missing_final_report
./workspace/evidence/access.log:3:2026-05-20 08:41:12 INFO login user=sora ip=10.0.0.12
./workspace/evidence/access.log:4:2026-05-20 08:41:20 INFO GET /project/assets 200 user=sora
./workspace/evidence/access.log:8:2026-05-20 08:43:27 INFO GET /project/screenshot.png 200 user=sora
./workspace/evidence/access.log:11:2026-05-20 08:45:31 INFO POST /upload 201 user=sora file=screen-main.png
./workspace/evidence/access.log:16:2026-05-20 08:48:45 INFO GET /project/assets 200 user=sora
./workspace/evidence/access.log:18:2026-05-20 08:49:53 INFO GET /project/final_report.md 404 user=sora
./workspace/evidence/access.log:19:2026-05-20 08:50:07 INFO POST /upload 201 user=sora file=team-photo.png
./workspace/evidence/access.log:21:2026-05-20 08:51:02 INFO POST /upload 201 user=sora file=final_report.md
./workspace/evidence/access.log:22:2026-05-20 08:51:22 INFO GET /project/final_report.md 200 user=sora
./workspace/evidence/access.log:28:2026-05-20 08:55:05 INFO GET /project/final_report.md 200 user=sora
./workspace/evidence/access.log:31:2026-05-20 08:56:18 INFO GET /project/final_report.md 404 user=sora
./workspace/evidence/access.log:34:2026-05-20 08:58:03 INFO GET /submit/status 200 user=sora
./workspace/evidence/access.log:35:2026-05-20 08:58:25 INFO GET /project/final_report.md 404 user=sora
./workspace/evidence/chat.log:2:2026-05-20 08:41 sora: 이미지 두 장만 더 올릴게.
./workspace/evidence/chat.log:5:2026-05-20 08:44 sora: 스크린샷 업로드 완료.
./workspace/evidence/chat.log:8:2026-05-20 08:47 sora: 아직 final_report 없어서 내가 올릴게.
./workspace/evidence/chat.log:9:2026-05-20 08:50 sora: final_report.md 업로드 준비 중.
./workspace/evidence/chat.log:10:2026-05-20 08:51 sora: final_report.md 올렸어.
./workspace/evidence/chat.log:15:2026-05-20 08:56 sora: 잠깐, final_report가 안 보여.
./workspace/evidence/chat.log:17:2026-05-20 08:58 sora: 제출 상태에 최종 보고서 누락이라고 나와.
./workspace/evidence/file-events.log:3:2026-05-20 08:41:30 OPEN project/assets/screen-main.png user=sora
./workspace/evidence/file-events.log:6:2026-05-20 08:44:12 UPLOAD project/assets/screen-main.png user=sora
./workspace/evidence/file-events.log:12:2026-05-20 08:50:07 UPLOAD project/assets/team-photo.png user=sora
./workspace/evidence/file-events.log:14:2026-05-20 08:51:02 UPLOAD project/final_report.md user=sora
./workspace/evidence/file-events.log:21:2026-05-20 08:55:03 OPEN project/final_report.md user=sora
./workspace/evidence/file-events.log:25:2026-05-20 08:56:18 CHECK project/final_report.md user=sora status=missing
./workspace/evidence/file-events.log:28:2026-05-20 08:58:03 CHECK submit/status user=sora status=missing_final_report
./case/suspects.md:13:## minho
./case-report-sample.md:70:evidence/access.log:30:2026-05-20 08:56:01 INFO POST /file/action 200 user=minho target=final_report.md result=removed
./case-report-sample.md:72:evidence/file-events.log:24:2026-05-20 08:56:01 FILE_EVENT target=project/final_report.md user=minho action=cleanup result=removed
./case-report-sample.md:85:grep -rn "minho" .
./case-report-sample.md:86:grep -rn "final_report" . | grep "minho"
./case-report-sample.md:87:grep -rni "removed" . | grep "minho"
./case-report-sample.md:93:evidence/chat.log:14:2026-05-20 08:55 minho: 제출 전에 파일 이름 정리할게.
./case-report-sample.md:94:evidence/chat.log:18:2026-05-20 08:59 minho: 미안, 정리하다가 잘못 눌렀을 수도 있어.
./case-report-sample.md:95:evidence/access.log:30:2026-05-20 08:56:01 INFO POST /file/action 200 user=minho target=final_report.md result=removed
./case-report-sample.md:96:evidence/file-events.log:24:2026-05-20 08:56:01 FILE_EVENT target=project/final_report.md user=minho action=cleanup result=removed
./case-report-sample.md:103:`evidence/file-events.log:24`에서 `minho`가 `project/final_report.md`에 대해
./case-report-sample.md:108:`minho`가 제출 전 파일 이름을 정리하던 중 `final_report.md`를 잘못 정리해서 사라진 것으로 보인다.
./case-report-sample.md:160:  18 user=minho
./check_report.py:113:            "`minho` 관련 단서가 있다.",
./check_report.py:115:            has_any(text, [r"minho"]),
./check_report.py:116:            "`grep -rn \"minho\" .` 또는 조합 검색 결과를 남긴다.",
./check_report.py:123:            and has_any(text, [r"minho", r"removed", r"cleanup", r"정리"]),
./evidence/access.log:5:2026-05-20 08:42:03 INFO login user=minho ip=10.0.0.13
./evidence/access.log:6:2026-05-20 08:42:19 INFO GET /project 200 user=minho
./evidence/access.log:9:2026-05-20 08:44:05 INFO GET /project/src/submit.py 200 user=minho
./evidence/access.log:15:2026-05-20 08:48:02 INFO GET /project/src/config.py 200 user=minho
./evidence/access.log:20:2026-05-20 08:50:29 INFO GET /project/src/submit.py 200 user=minho
./evidence/access.log:24:2026-05-20 08:52:41 INFO GET /project/final_report.md 200 user=minho
./evidence/access.log:25:2026-05-20 08:53:20 INFO GET /project 200 user=minho
./evidence/access.log:29:2026-05-20 08:55:33 INFO GET /project 200 user=minho
./evidence/access.log:30:2026-05-20 08:56:01 INFO POST /file/action 200 user=minho target=final_report.md result=removed
./evidence/access.log:33:2026-05-20 08:57:44 INFO GET /project 200 user=minho
./evidence/chat.log:3:2026-05-20 08:42 minho: 제출 스크립트 한번 확인해볼게.
./evidence/chat.log:6:2026-05-20 08:45 minho: 파일 이름 규칙이 final_report.md 맞지?
./evidence/chat.log:12:2026-05-20 08:53 minho: 나도 확인했어.
./evidence/chat.log:14:2026-05-20 08:55 minho: 제출 전에 파일 이름 정리할게.
./evidence/chat.log:18:2026-05-20 08:59 minho: 미안, 정리하다가 잘못 눌렀을 수도 있어.
./evidence/file-events.log:4:2026-05-20 08:42:10 OPEN project/src/submit.py user=minho
./evidence/file-events.log:8:2026-05-20 08:46:22 OPEN project/src/config.py user=minho
./evidence/file-events.log:13:2026-05-20 08:50:29 OPEN project/src/submit.py user=minho
./evidence/file-events.log:17:2026-05-20 08:52:41 OPEN project/final_report.md user=minho
./evidence/file-events.log:22:2026-05-20 08:55:33 LIST project/ user=minho
./evidence/file-events.log:23:2026-05-20 08:55:50 RENAME project/final-report.md project/final_report.md user=minho status=failed
./evidence/file-events.log:24:2026-05-20 08:56:01 FILE_EVENT target=project/final_report.md user=minho action=cleanup result=removed
./evidence/file-events.log:27:2026-05-20 08:57:44 LIST project/ user=minho
./README.md:38:- `minho` 관련 단서와 결론 문장
./workspace/evidence/access.log:5:2026-05-20 08:42:03 INFO login user=minho ip=10.0.0.13
./workspace/evidence/access.log:6:2026-05-20 08:42:19 INFO GET /project 200 user=minho
./workspace/evidence/access.log:9:2026-05-20 08:44:05 INFO GET /project/src/submit.py 200 user=minho
./workspace/evidence/access.log:15:2026-05-20 08:48:02 INFO GET /project/src/config.py 200 user=minho
./workspace/evidence/access.log:20:2026-05-20 08:50:29 INFO GET /project/src/submit.py 200 user=minho
./workspace/evidence/access.log:24:2026-05-20 08:52:41 INFO GET /project/final_report.md 200 user=minho
./workspace/evidence/access.log:25:2026-05-20 08:53:20 INFO GET /project 200 user=minho
./workspace/evidence/access.log:29:2026-05-20 08:55:33 INFO GET /project 200 user=minho
./workspace/evidence/access.log:30:2026-05-20 08:56:01 INFO POST /file/action 200 user=minho target=final_report.md result=removed
./workspace/evidence/access.log:33:2026-05-20 08:57:44 INFO GET /project 200 user=minho
./workspace/evidence/chat.log:3:2026-05-20 08:42 minho: 제출 스크립트 한번 확인해볼게.
./workspace/evidence/chat.log:6:2026-05-20 08:45 minho: 파일 이름 규칙이 final_report.md 맞지?
./workspace/evidence/chat.log:12:2026-05-20 08:53 minho: 나도 확인했어.
./workspace/evidence/chat.log:14:2026-05-20 08:55 minho: 제출 전에 파일 이름 정리할게.
./workspace/evidence/chat.log:18:2026-05-20 08:59 minho: 미안, 정리하다가 잘못 눌렀을 수도 있어.
./workspace/evidence/file-events.log:4:2026-05-20 08:42:10 OPEN project/src/submit.py user=minho
./workspace/evidence/file-events.log:8:2026-05-20 08:46:22 OPEN project/src/config.py user=minho
./workspace/evidence/file-events.log:13:2026-05-20 08:50:29 OPEN project/src/submit.py user=minho
./workspace/evidence/file-events.log:17:2026-05-20 08:52:41 OPEN project/final_report.md user=minho
./workspace/evidence/file-events.log:22:2026-05-20 08:55:33 LIST project/ user=minho
./workspace/evidence/file-events.log:23:2026-05-20 08:55:50 RENAME project/final-report.md project/final_report.md user=minho status=failed
./workspace/evidence/file-events.log:24:2026-05-20 08:56:01 FILE_EVENT target=project/final_report.md user=minho action=cleanup result=removed
./workspace/evidence/file-events.log:27:2026-05-20 08:57:44 LIST project/ user=minho
Binary file ./.git/index matches
./case/briefing.md:3:캠퍼스 해커톤 마감 10분 전, Team Nova의 `final_report.md`가 제출 폴더에서 사라졌습니다.
./case/briefing.md:9:- `final_report.md`가 언제 사라졌는지 찾기
./case/suspects.md:11:- `final_report.md`를 검토했다.
./case/timeline.md:5:- 08:51 `final_report.md`가 업로드됐다.
./case/timeline.md:7:- 08:56 `final_report.md` 파일이 보이지 않는 상태가 기록됐다.
./case-report-sample.md:47:final_report.md
./case-report-sample.md:53:캠퍼스 해커톤 마감 직전 `project/final_report.md`가 사라진 사건이다.
./case-report-sample.md:55:로그에서 `final_report`의 업로드, 삭제 또는 누락, 복구 흐름을 확인해야 한다.
./case-report-sample.md:62:grep -n "final_report" evidence/*.log
./case-report-sample.md:70:evidence/access.log:30:2026-05-20 08:56:01 INFO POST /file/action 200 user=minho target=final_report.md result=removed
./case-report-sample.md:71:evidence/file-events.log:14:2026-05-20 08:51:02 UPLOAD project/final_report.md user=sora
./case-report-sample.md:72:evidence/file-events.log:24:2026-05-20 08:56:01 FILE_EVENT target=project/final_report.md user=minho action=cleanup result=removed
./case-report-sample.md:73:evidence/file-events.log:25:2026-05-20 08:56:18 CHECK project/final_report.md user=sora status=missing
./case-report-sample.md:74:evidence/file-events.log:26:2026-05-20 08:57:02 CHECK project/final_report.md user=jimin status=missing
./case-report-sample.md:75:evidence/file-events.log:29:2026-05-20 08:58:20 RESTORE project/final_report.md user=admin source=backup
./case-report-sample.md:86:grep -rn "final_report" . | grep "minho"
./case-report-sample.md:95:evidence/access.log:30:2026-05-20 08:56:01 INFO POST /file/action 200 user=minho target=final_report.md result=removed
./case-report-sample.md:96:evidence/file-events.log:24:2026-05-20 08:56:01 FILE_EVENT target=project/final_report.md user=minho action=cleanup result=removed
./case-report-sample.md:103:`evidence/file-events.log:24`에서 `minho`가 `project/final_report.md`에 대해
./case-report-sample.md:108:`minho`가 제출 전 파일 이름을 정리하던 중 `final_report.md`를 잘못 정리해서 사라진 것으로 보인다.
./case-report-sample.md:165:### final_report 사건 흐름
./check_report.py:92:            "`final_report` 관련 내용이 있다.",
./check_report.py:94:            has_any(text, [r"final_report", r"final-report"]),
./check_report.py:95:            "`final_report`를 검색한 결과를 보고서에 남긴다.",
./evidence/access.log:12:2026-05-20 08:46:10 INFO GET /project/final_report.md 404 user=jimin
./evidence/access.log:18:2026-05-20 08:49:53 INFO GET /project/final_report.md 404 user=sora
./evidence/access.log:21:2026-05-20 08:51:02 INFO POST /upload 201 user=sora file=final_report.md
./evidence/access.log:22:2026-05-20 08:51:22 INFO GET /project/final_report.md 200 user=sora
./evidence/access.log:23:2026-05-20 08:52:03 INFO GET /project/final_report.md 200 user=jimin
./evidence/access.log:24:2026-05-20 08:52:41 INFO GET /project/final_report.md 200 user=minho
./evidence/access.log:28:2026-05-20 08:55:05 INFO GET /project/final_report.md 200 user=sora
./evidence/access.log:30:2026-05-20 08:56:01 INFO POST /file/action 200 user=minho target=final_report.md result=removed
./evidence/access.log:31:2026-05-20 08:56:18 INFO GET /project/final_report.md 404 user=sora
./evidence/access.log:32:2026-05-20 08:57:02 INFO GET /project/final_report.md 404 user=jimin
./evidence/access.log:35:2026-05-20 08:58:25 INFO GET /project/final_report.md 404 user=sora
./evidence/chat.log:6:2026-05-20 08:45 minho: 파일 이름 규칙이 final_report.md 맞지?
./evidence/chat.log:7:2026-05-20 08:46 jimin: 응. 마지막 파일은 final_report.md.
./evidence/chat.log:8:2026-05-20 08:47 sora: 아직 final_report 없어서 내가 올릴게.
./evidence/chat.log:9:2026-05-20 08:50 sora: final_report.md 업로드 준비 중.
./evidence/chat.log:10:2026-05-20 08:51 sora: final_report.md 올렸어.
./evidence/chat.log:15:2026-05-20 08:56 sora: 잠깐, final_report가 안 보여.
./evidence/file-events.log:14:2026-05-20 08:51:02 UPLOAD project/final_report.md user=sora
./evidence/file-events.log:15:2026-05-20 08:51:20 CHECK project/final_report.md user=system
./evidence/file-events.log:16:2026-05-20 08:52:03 OPEN project/final_report.md user=jimin
./evidence/file-events.log:17:2026-05-20 08:52:41 OPEN project/final_report.md user=minho
./evidence/file-events.log:18:2026-05-20 08:53:11 COPY project/final_report.md project/final_report_backup.md user=system
./evidence/file-events.log:21:2026-05-20 08:55:03 OPEN project/final_report.md user=sora
./evidence/file-events.log:23:2026-05-20 08:55:50 RENAME project/final-report.md project/final_report.md user=minho status=failed
./evidence/file-events.log:24:2026-05-20 08:56:01 FILE_EVENT target=project/final_report.md user=minho action=cleanup result=removed
./evidence/file-events.log:25:2026-05-20 08:56:18 CHECK project/final_report.md user=sora status=missing
./evidence/file-events.log:26:2026-05-20 08:57:02 CHECK project/final_report.md user=jimin status=missing
./evidence/file-events.log:28:2026-05-20 08:58:03 CHECK submit/status user=sora status=missing_final_report
./evidence/file-events.log:29:2026-05-20 08:58:20 RESTORE project/final_report.md user=admin source=backup
./project/src/config.py:2:FINAL_REPORT = "final_report.md"
./README.md:5:캠퍼스 해커톤 마감 직전 `project/final_report.md`가 사라졌습니다.
./README.md:36:- `final_report`, `removed`, `missing` 관련 로그 근거
./workspace/evidence/access.log:12:2026-05-20 08:46:10 INFO GET /project/final_report.md 404 user=jimin
./workspace/evidence/access.log:18:2026-05-20 08:49:53 INFO GET /project/final_report.md 404 user=sora
./workspace/evidence/access.log:21:2026-05-20 08:51:02 INFO POST /upload 201 user=sora file=final_report.md
./workspace/evidence/access.log:22:2026-05-20 08:51:22 INFO GET /project/final_report.md 200 user=sora
./workspace/evidence/access.log:23:2026-05-20 08:52:03 INFO GET /project/final_report.md 200 user=jimin
./workspace/evidence/access.log:24:2026-05-20 08:52:41 INFO GET /project/final_report.md 200 user=minho
./workspace/evidence/access.log:28:2026-05-20 08:55:05 INFO GET /project/final_report.md 200 user=sora
./workspace/evidence/access.log:30:2026-05-20 08:56:01 INFO POST /file/action 200 user=minho target=final_report.md result=removed
./workspace/evidence/access.log:31:2026-05-20 08:56:18 INFO GET /project/final_report.md 404 user=sora
./workspace/evidence/access.log:32:2026-05-20 08:57:02 INFO GET /project/final_report.md 404 user=jimin
./workspace/evidence/access.log:35:2026-05-20 08:58:25 INFO GET /project/final_report.md 404 user=sora
./workspace/evidence/chat.log:6:2026-05-20 08:45 minho: 파일 이름 규칙이 final_report.md 맞지?
./workspace/evidence/chat.log:7:2026-05-20 08:46 jimin: 응. 마지막 파일은 final_report.md.
./workspace/evidence/chat.log:8:2026-05-20 08:47 sora: 아직 final_report 없어서 내가 올릴게.
./workspace/evidence/chat.log:9:2026-05-20 08:50 sora: final_report.md 업로드 준비 중.
./workspace/evidence/chat.log:10:2026-05-20 08:51 sora: final_report.md 올렸어.
./workspace/evidence/chat.log:15:2026-05-20 08:56 sora: 잠깐, final_report가 안 보여.
./workspace/evidence/file-events.log:14:2026-05-20 08:51:02 UPLOAD project/final_report.md user=sora
./workspace/evidence/file-events.log:15:2026-05-20 08:51:20 CHECK project/final_report.md user=system
./workspace/evidence/file-events.log:16:2026-05-20 08:52:03 OPEN project/final_report.md user=jimin
./workspace/evidence/file-events.log:17:2026-05-20 08:52:41 OPEN project/final_report.md user=minho
./workspace/evidence/file-events.log:18:2026-05-20 08:53:11 COPY project/final_report.md project/final_report_backup.md user=system
./workspace/evidence/file-events.log:21:2026-05-20 08:55:03 OPEN project/final_report.md user=sora
./workspace/evidence/file-events.log:23:2026-05-20 08:55:50 RENAME project/final-report.md project/final_report.md user=minho status=failed
./workspace/evidence/file-events.log:24:2026-05-20 08:56:01 FILE_EVENT target=project/final_report.md user=minho action=cleanup result=removed
./workspace/evidence/file-events.log:25:2026-05-20 08:56:18 CHECK project/final_report.md user=sora status=missing
./workspace/evidence/file-events.log:26:2026-05-20 08:57:02 CHECK project/final_report.md user=jimin status=missing
./workspace/evidence/file-events.log:28:2026-05-20 08:58:03 CHECK submit/status user=sora status=missing_final_report
./workspace/evidence/file-events.log:29:2026-05-20 08:58:20 RESTORE project/final_report.md user=admin source=backup
./workspace/notes/case-briefing.md:3:캠퍼스 해커톤 마감 10분 전, Team Nova의 `final_report.md`가 제출 폴더에서 사라졌습니다.
./workspace/notes/case-briefing.md:9:- `final_report.md`가 언제 사라졌는지 찾기
Binary file ./.git/index matches
./case/suspects.md:6:- 마감 전에 `draft_report.md`를 열어봤다.
./case/timeline.md:4:- 08:47 `draft_report.md`가 수정됐다.
./case-report-sample.md:46:draft_report.md
./evidence/access.log:7:2026-05-20 08:43:01 INFO GET /project/draft_report.md 200 user=jimin
./evidence/access.log:10:2026-05-20 08:44:58 INFO GET /project/draft_report.md 200 user=jimin
./evidence/access.log:13:2026-05-20 08:46:44 INFO GET /project/draft_report.md 200 user=jimin
./evidence/access.log:14:2026-05-20 08:47:18 INFO POST /save 200 user=jimin file=draft_report.md
./evidence/access.log:17:2026-05-20 08:49:11 INFO GET /project/draft_report.md 200 user=jimin
./evidence/access.log:26:2026-05-20 08:54:06 INFO GET /project/draft_report.md 200 user=jimin
./evidence/access.log:27:2026-05-20 08:54:39 INFO POST /save 200 user=jimin file=draft_report.md
./evidence/access.log:36:2026-05-20 08:59:10 INFO GET /project/draft_report.md 200 user=jimin
./evidence/chat.log:4:2026-05-20 08:43 jimin: draft_report.md 문장 조금 고쳤어.
./evidence/file-events.log:2:2026-05-20 08:41:01 OPEN project/draft_report.md user=jimin
./evidence/file-events.log:5:2026-05-20 08:43:03 SAVE project/draft_report.md user=jimin
./evidence/file-events.log:9:2026-05-20 08:47:18 SAVE project/draft_report.md user=jimin
./evidence/file-events.log:10:2026-05-20 08:48:05 OPEN project/draft_report.md user=jimin
./evidence/file-events.log:11:2026-05-20 08:49:07 SAVE project/draft_report.md user=jimin
./evidence/file-events.log:19:2026-05-20 08:54:06 OPEN project/draft_report.md user=jimin
./evidence/file-events.log:20:2026-05-20 08:54:39 SAVE project/draft_report.md user=jimin
./evidence/file-events.log:30:2026-05-20 08:59:10 OPEN project/draft_report.md user=jimin
./project/src/config.py:3:DRAFT_REPORT = "draft_report.md"
./workspace/evidence/access.log:7:2026-05-20 08:43:01 INFO GET /project/draft_report.md 200 user=jimin
./workspace/evidence/access.log:10:2026-05-20 08:44:58 INFO GET /project/draft_report.md 200 user=jimin
./workspace/evidence/access.log:13:2026-05-20 08:46:44 INFO GET /project/draft_report.md 200 user=jimin
./workspace/evidence/access.log:14:2026-05-20 08:47:18 INFO POST /save 200 user=jimin file=draft_report.md
./workspace/evidence/access.log:17:2026-05-20 08:49:11 INFO GET /project/draft_report.md 200 user=jimin
./workspace/evidence/access.log:26:2026-05-20 08:54:06 INFO GET /project/draft_report.md 200 user=jimin
./workspace/evidence/access.log:27:2026-05-20 08:54:39 INFO POST /save 200 user=jimin file=draft_report.md
./workspace/evidence/access.log:36:2026-05-20 08:59:10 INFO GET /project/draft_report.md 200 user=jimin
./workspace/evidence/chat.log:4:2026-05-20 08:43 jimin: draft_report.md 문장 조금 고쳤어.
./workspace/evidence/file-events.log:2:2026-05-20 08:41:01 OPEN project/draft_report.md user=jimin
./workspace/evidence/file-events.log:5:2026-05-20 08:43:03 SAVE project/draft_report.md user=jimin
./workspace/evidence/file-events.log:9:2026-05-20 08:47:18 SAVE project/draft_report.md user=jimin
./workspace/evidence/file-events.log:10:2026-05-20 08:48:05 OPEN project/draft_report.md user=jimin
./workspace/evidence/file-events.log:11:2026-05-20 08:49:07 SAVE project/draft_report.md user=jimin
./workspace/evidence/file-events.log:19:2026-05-20 08:54:06 OPEN project/draft_report.md user=jimin
./workspace/evidence/file-events.log:20:2026-05-20 08:54:39 SAVE project/draft_report.md user=jimin
./workspace/evidence/file-events.log:30:2026-05-20 08:59:10 OPEN project/draft_report.md user=jimin
./case-report-sample.md:63:grep -ni "removed" evidence/*.log
./case-report-sample.md:70:evidence/access.log:30:2026-05-20 08:56:01 INFO POST /file/action 200 user=minho target=final_report.md result=removed
./case-report-sample.md:72:evidence/file-events.log:24:2026-05-20 08:56:01 FILE_EVENT target=project/final_report.md user=minho action=cleanup result=removed
./case-report-sample.md:87:grep -rni "removed" . | grep "minho"
./case-report-sample.md:95:evidence/access.log:30:2026-05-20 08:56:01 INFO POST /file/action 200 user=minho target=final_report.md result=removed
./case-report-sample.md:96:evidence/file-events.log:24:2026-05-20 08:56:01 FILE_EVENT target=project/final_report.md user=minho action=cleanup result=removed
./case-report-sample.md:104:`action=cleanup result=removed`를 만든 기록이 있다.
./case-report-sample.md:114:하지만 `removed`, `missing`, `RESTORE` 흐름은 사라짐과 복구가 있었음을 보여준다.
./case-report-sample.md:173:grep -En "UPLOAD|RESTORE|removed|missing" evidence/*.log
./check_report.py:99:            "`removed`와 `missing` 기록이 모두 있다.",
./check_report.py:101:            has_any(text, [r"removed"]) and has_any(text, [r"missing"]),
./check_report.py:102:            "`grep -ni \"removed\" evidence/*.log`, `grep -ni \"missing\" evidence/*.log` 결과를 남긴다.",
./check_report.py:123:            and has_any(text, [r"minho", r"removed", r"cleanup", r"정리"]),
./evidence/access.log:30:2026-05-20 08:56:01 INFO POST /file/action 200 user=minho target=final_report.md result=removed
./evidence/file-events.log:24:2026-05-20 08:56:01 FILE_EVENT target=project/final_report.md user=minho action=cleanup result=removed
./README.md:13:- `evidence/*.log`의 UPLOAD, RESTORE, missing, removed 기록
./README.md:36:- `final_report`, `removed`, `missing` 관련 로그 근거
./workspace/evidence/access.log:30:2026-05-20 08:56:01 INFO POST /file/action 200 user=minho target=final_report.md result=removed
./workspace/evidence/file-events.log:24:2026-05-20 08:56:01 FILE_EVENT target=project/final_report.md user=minho action=cleanup result=removed
./.github/workflows/check-report.yml:82:      - name: Fail when required checks are missing
./case-report-sample.md:64:grep -ni "missing" evidence/*.log
./case-report-sample.md:73:evidence/file-events.log:25:2026-05-20 08:56:18 CHECK project/final_report.md user=sora status=missing
./case-report-sample.md:74:evidence/file-events.log:26:2026-05-20 08:57:02 CHECK project/final_report.md user=jimin status=missing
./case-report-sample.md:114:하지만 `removed`, `missing`, `RESTORE` 흐름은 사라짐과 복구가 있었음을 보여준다.
./case-report-sample.md:173:grep -En "UPLOAD|RESTORE|removed|missing" evidence/*.log
./check_report.py:99:            "`removed`와 `missing` 기록이 모두 있다.",
./check_report.py:101:            has_any(text, [r"removed"]) and has_any(text, [r"missing"]),
./check_report.py:102:            "`grep -ni \"removed\" evidence/*.log`, `grep -ni \"missing\" evidence/*.log` 결과를 남긴다.",
./evidence/file-events.log:25:2026-05-20 08:56:18 CHECK project/final_report.md user=sora status=missing
./evidence/file-events.log:26:2026-05-20 08:57:02 CHECK project/final_report.md user=jimin status=missing
./evidence/file-events.log:28:2026-05-20 08:58:03 CHECK submit/status user=sora status=missing_final_report
./README.md:13:- `evidence/*.log`의 UPLOAD, RESTORE, missing, removed 기록
./README.md:36:- `final_report`, `removed`, `missing` 관련 로그 근거
./workspace/evidence/file-events.log:25:2026-05-20 08:56:18 CHECK project/final_report.md user=sora status=missing
./workspace/evidence/file-events.log:26:2026-05-20 08:57:02 CHECK project/final_report.md user=jimin status=missing
./workspace/evidence/file-events.log:28:2026-05-20 08:58:03 CHECK submit/status user=sora status=missing_final_report
unknown 검색 결과 없음

## 8. 오늘 사용한 명령어
  473  grep -rn "sora" . >> case-report.md
  474  grep -rn "minho" . >> case-report.md 
  475  grep -rn "final_report" . >> case-report.md
  476  grep -rn "draft_report" . >> case-report.md
  477  grep -rni "removed" . >> case-report.md
  478  grep -rni "missing" . >> case-report.md
  479  grep -rn "unknown" .
  480  echo "unknown 검색 결과 없음" >> case-report.md
  481  echo "## 8. 오늘 사용한 명령어" >> case-report.md
  482  history | tail >> case-report.md

결론:
file-events.log의 removed 기록과 chat.log의 대화 기록을 보면
final_report.md는 마감 직전에 삭제된 것으로 보인다.
가장 중요한 단서는 file-events.log의 result=removed 줄이다.

## Appendix. 추가 분석
### 사용자별 활동량
      3 user=admin
     23 user=jimin
     18 user=minho
     20 user=sora
      4 user=system
### final_report 사건 흐름
evidence/access.log:30:2026-05-20 08:56:01 INFO POST /file/action 200 user=minho target=final_report.md result=removed
evidence/file-events.log:6:2026-05-20 08:44:12 UPLOAD project/assets/screen-main.png user=sora
evidence/file-events.log:12:2026-05-20 08:50:07 UPLOAD project/assets/team-photo.png user=sora
evidence/file-events.log:14:2026-05-20 08:51:02 UPLOAD project/final_report.md user=sora
evidence/file-events.log:24:2026-05-20 08:56:01 FILE_EVENT target=project/final_report.md user=minho action=cleanup result=removed
evidence/file-events.log:25:2026-05-20 08:56:18 CHECK project/final_report.md user=sora status=missing
evidence/file-events.log:26:2026-05-20 08:57:02 CHECK project/final_report.md user=jimin status=missing
evidence/file-events.log:28:2026-05-20 08:58:03 CHECK submit/status user=sora status=missing_final_report
evidence/file-events.log:29:2026-05-20 08:58:20 RESTORE project/final_report.md user=admin source=backup
