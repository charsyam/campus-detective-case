# 사건 조사 보고서

## 1. 현재 위치

명령어:

결과:

## 2. 사건 자료 목록

명령어:

결과:

## 3. 사건 개요

요약:

## 4. 로그 증거

명령어:

발견한 줄:

## 5. 용의자별 단서

명령어:

검색 결과:

## 6. 결론

가장 중요한 증거:

가장 의심되는 상황:

아직 확실하지 않은 점:

## 7. Git 저장 결과

브랜치:

커밋:

## 8. 오늘 사용한 명령어

-
-
-

## 1. 현재 위치
/c/Users/heo01/campus-detective-case
## 2. 사건 자료 목록
total 45
drwxr-xr-x 1 jae11 197609    0 May 22 14:20 ./
drwxr-xr-x 1 jae11 197609    0 May 22 14:33 ../
drwxr-xr-x 1 jae11 197609    0 May 22 14:13 .git/
drwxr-xr-x 1 jae11 197609    0 May 22 14:10 .github/
-rw-r--r-- 1 jae11 197609 1252 May 22 14:10 README.md
drwxr-xr-x 1 jae11 197609    0 May 22 14:10 case/
-rw-r--r-- 1 jae11 197609 3828 May 22 14:10 case-report-sample.md
-rw-r--r-- 1 jae11 197609  575 May 22 14:38 case-report.md
-rwxr-xr-x 1 jae11 197609 7637 May 22 14:10 check_report.py*
drwxr-xr-x 1 jae11 197609    0 May 22 14:10 docs/
drwxr-xr-x 1 jae11 197609    0 May 22 14:10 evidence/
drwxr-xr-x 1 jae11 197609    0 May 22 14:10 project/
drwxr-xr-x 1 jae11 197609    0 May 22 14:27 workspace/
## 2-1. 폴더별 자료 목룍
### case
briefing.md
suspects.md
timeline.md
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

##4. 로그 증거
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
case/suspects.md:3:## jimin
case-report-sample.md:74:evidence/file-events.log:26:2026-05-20 08:57:02 CHECK project/final_report.md user=jimin status=missing
case-report-sample.md:83:grep -rn "jimin" .
case-report-sample.md:159:  23 user=jimin
evidence/access.log:1:2026-05-20 08:40:01 INFO login user=jimin ip=10.0.0.11
evidence/access.log:2:2026-05-20 08:40:09 INFO GET /project 200 user=jimin
evidence/access.log:7:2026-05-20 08:43:01 INFO GET /project/draft_report.md 200 user=jimin
evidence/access.log:10:2026-05-20 08:44:58 INFO GET /project/draft_report.md 200 user=jimin
evidence/access.log:12:2026-05-20 08:46:10 INFO GET /project/final_report.md 404 user=jimin
evidence/access.log:13:2026-05-20 08:46:44 INFO GET /project/draft_report.md 200 user=jimin
evidence/access.log:14:2026-05-20 08:47:18 INFO POST /save 200 user=jimin file=draft_report.md
evidence/access.log:17:2026-05-20 08:49:11 INFO GET /project/draft_report.md 200 user=jimin
evidence/access.log:23:2026-05-20 08:52:03 INFO GET /project/final_report.md 200 user=jimin
evidence/access.log:26:2026-05-20 08:54:06 INFO GET /project/draft_report.md 200 user=jimin
evidence/access.log:27:2026-05-20 08:54:39 INFO POST /save 200 user=jimin file=draft_report.md
evidence/access.log:32:2026-05-20 08:57:02 INFO GET /project/final_report.md 404 user=jimin
evidence/access.log:36:2026-05-20 08:59:10 INFO GET /project/draft_report.md 200 user=jimin
evidence/chat.log:1:2026-05-20 08:40 jimin: 발표 순서 확인했어.
evidence/chat.log:4:2026-05-20 08:43 jimin: draft_report.md 문장 조금 고쳤어.
evidence/chat.log:7:2026-05-20 08:46 jimin: 응. 마지막 파일은 final_report.md.
evidence/chat.log:11:2026-05-20 08:52 jimin: 열어보니 내용 괜찮아.
evidence/chat.log:13:2026-05-20 08:54 jimin: deadline 전에 draft는 남겨둬도 되나?
evidence/chat.log:16:2026-05-20 08:57 jimin: 나도 404가 떠.
evidence/file-events.log:2:2026-05-20 08:41:01 OPEN project/draft_report.md user=jimin
evidence/file-events.log:5:2026-05-20 08:43:03 SAVE project/draft_report.md user=jimin
evidence/file-events.log:9:2026-05-20 08:47:18 SAVE project/draft_report.md user=jimin
evidence/file-events.log:10:2026-05-20 08:48:05 OPEN project/draft_report.md user=jimin
evidence/file-events.log:11:2026-05-20 08:49:07 SAVE project/draft_report.md user=jimin
evidence/file-events.log:16:2026-05-20 08:52:03 OPEN project/final_report.md user=jimin
evidence/file-events.log:19:2026-05-20 08:54:06 OPEN project/draft_report.md user=jimin
evidence/file-events.log:20:2026-05-20 08:54:39 SAVE project/draft_report.md user=jimin
evidence/file-events.log:26:2026-05-20 08:57:02 CHECK project/final_report.md user=jimin status=missing
evidence/file-events.log:30:2026-05-20 08:59:10 OPEN project/draft_report.md user=jimin
workspace/evidence/access.log:1:2026-05-20 08:40:01 INFO login user=jimin ip=10.0.0.11
workspace/evidence/access.log:2:2026-05-20 08:40:09 INFO GET /project 200 user=jimin
workspace/evidence/access.log:7:2026-05-20 08:43:01 INFO GET /project/draft_report.md 200 user=jimin
workspace/evidence/access.log:10:2026-05-20 08:44:58 INFO GET /project/draft_report.md 200 user=jimin
workspace/evidence/access.log:12:2026-05-20 08:46:10 INFO GET /project/final_report.md 404 user=jimin
workspace/evidence/access.log:13:2026-05-20 08:46:44 INFO GET /project/draft_report.md 200 user=jimin
workspace/evidence/access.log:14:2026-05-20 08:47:18 INFO POST /save 200 user=jimin file=draft_report.md
workspace/evidence/access.log:17:2026-05-20 08:49:11 INFO GET /project/draft_report.md 200 user=jimin
workspace/evidence/access.log:23:2026-05-20 08:52:03 INFO GET /project/final_report.md 200 user=jimin
workspace/evidence/access.log:26:2026-05-20 08:54:06 INFO GET /project/draft_report.md 200 user=jimin
workspace/evidence/access.log:27:2026-05-20 08:54:39 INFO POST /save 200 user=jimin file=draft_report.md
workspace/evidence/access.log:32:2026-05-20 08:57:02 INFO GET /project/final_report.md 404 user=jimin
workspace/evidence/access.log:36:2026-05-20 08:59:10 INFO GET /project/draft_report.md 200 user=jimin
workspace/evidence/chat.log:1:2026-05-20 08:40 jimin: 발표 순서 확인했어.
workspace/evidence/chat.log:4:2026-05-20 08:43 jimin: draft_report.md 문장 조금 고쳤어.
workspace/evidence/chat.log:7:2026-05-20 08:46 jimin: 응. 마지막 파일은 final_report.md.
workspace/evidence/chat.log:11:2026-05-20 08:52 jimin: 열어보니 내용 괜찮아.
workspace/evidence/chat.log:13:2026-05-20 08:54 jimin: deadline 전에 draft는 남겨둬도 되나?
workspace/evidence/chat.log:16:2026-05-20 08:57 jimin: 나도 404가 떠.
workspace/evidence/file-events.log:2:2026-05-20 08:41:01 OPEN project/draft_report.md user=jimin
workspace/evidence/file-events.log:5:2026-05-20 08:43:03 SAVE project/draft_report.md user=jimin
workspace/evidence/file-events.log:9:2026-05-20 08:47:18 SAVE project/draft_report.md user=jimin
workspace/evidence/file-events.log:10:2026-05-20 08:48:05 OPEN project/draft_report.md user=jimin
workspace/evidence/file-events.log:11:2026-05-20 08:49:07 SAVE project/draft_report.md user=jimin
workspace/evidence/file-events.log:16:2026-05-20 08:52:03 OPEN project/final_report.md user=jimin
workspace/evidence/file-events.log:19:2026-05-20 08:54:06 OPEN project/draft_report.md user=jimin
workspace/evidence/file-events.log:20:2026-05-20 08:54:39 SAVE project/draft_report.md user=jimin
workspace/evidence/file-events.log:26:2026-05-20 08:57:02 CHECK project/final_report.md user=jimin status=missing
workspace/evidence/file-events.log:30:2026-05-20 08:59:10 OPEN project/draft_report.md user=jimin
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
./workspace/evidence/file-events.log:30:2026-05-20 08:59:10 OPEN project/draft_report.md user=jimin
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
./workspace/evidence/file-events.log:30:2026-05-20 08:59:10 OPEN project/draft_report.md user=jimin
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

## 6. 결론

가장 중요한 증거: evidence/file-events.log:24:2026-05-20 08:56:01 FILE_EVENT target=project/final_report.md user=minho action=cleanup result=removed

가장 의심되는 상황: `minho`가 제출 전 파일 이름을 정리하던 중 `final_report.md`를 잘못 정리해서 사라진 것으로 보인다.

아직 확실하지 않은 점: 
## 8. 오늘 사용한 멸령어
  129  grep -rn "minho" . case-report.md
  130  grep -rn "minho" .
  131  pwed
  132  pwd
  133  cat case-report.md
  134  grep -n "removed" case-report.md
  135  grep -n "fianl_report" case-report.md
  136  grep -n "final_report" case-report.md
  137  echo "## 8. 오늘 사용한 멸령어" >> case-report.md
  138  history | tail >> case-report.md
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
