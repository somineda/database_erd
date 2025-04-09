# 🗂 Recruitment Platform Database Schema

이 프로젝트는 프로그래머스 채용공고 부분 백엔드 데이터베이스 설계 구조

---

## 📌 주요 개념 및 설계 목적

- 사용자 역할 분리: `applicant`, `recruiter`
- 프로필 상세 정보는 역할에 따라 분리 테이블 사용
- 하나의 회사에 여러 채용담당자 연결 가능 (N:M 관계)
- 채용공고 북마크 기능, 지원 기능, 이력서 연결 포함
- 모든 테이블에 `updated_at` 필드 포함 (변경 추적 목적)

---

## 🧱 테이블 구성 요약

### 🔹 `user`
- 지원자/채용담당자 공통 계정
- role: 'applicant' or 'recruiter'

### 🔹 `applicant_profile`
- 지원자 자기소개 정보

### 🔹 `recruiter_profile`
- 채용담당자 정보

### 🔹 `company`
- 회사 정보 

### 🔹 `recruiter_company`
- 다대다 관계 테이블: 채용담당자 ↔ 회사

### 🔹 `category`
- 채용공고 직무 분류

### 🔹 `resume`
- 사용자가 작성한 이력서

### 🔹 `job_posting`
- 등록된 채용공고
- 최소/최대 연봉 필드 분리

### 🔹 `application`
- 사용자 지원 내역

### 🔹 `bookmark`
- 채용공고 북마크

---

## 🔗 테이블 간 관계

| 관계 | 설명 |
|------|------|
| `user` 1:1 `applicant_profile` | 지원자 역할 프로필 연결 |
| `user` 1:1 `recruiter_profile` | 채용담당자 역할 프로필 연결 |
| `user` 1:N `resume` | 한 사용자가 여러 이력서 작성 가능 |
| `user` 1:N `application` | 한 사용자가 여러 공고에 지원 가능 |
| `user` 1:N `bookmark` | 한 사용자가 여러 공고 북마크 가능 |
| `user` N:M `company` → `recruiter_company` | 채용담당자 ↔ 회사 |
| `company` 1:N `job_posting` | 하나의 회사가 여러 공고 등록 가능 |
| `job_posting` 1:N `application` | 하나의 공고에 여러 유저가 지원 가능 |
| `resume` 1:N `application` | 하나의 이력서를 여러 지원서에 사용 가능 |
| `job_posting` 1:N `bookmark` | 하나의 공고가 여러 유저에게 북마크 될 수 있음 |

---


