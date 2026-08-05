# uvicorn -> Swagger UI, ReDoc API 명세서
해당 내용은 api-test01을 기반으로 합니다.

## 레포 WSL 기반 VScode에 불러오기
1. 깃허브에 존재하는 레포 VS code에 불러오기
```
git clone https://github.com/rkdalstjr/<레포이름>.git
```
2. 레포 폴더를 왼쪽 EXPLORER 폴더와 호환시키기

## 가상환경(.venv) 설정 방법
1. 프로젝트 가상환경 생성
```
cd ~/api-test01
python3 -m venv .venv
```

2. 가상환경 활성화
```
source .venv/bin/activate
```

3. 패키지 설치
```
pip install fastapi uvicorn
```

4. 가상환경 비활성화 (굳이 하지 않아도 됨)
```
deactivate
```

## 레포 기본 양식
- .venv
- .gitignore
- .key
- LICENSE
- main.py
- README.md
- requirements.txt

## uvicorn 서버 실행 방법
```
uvicorn main:app --reload
```

## API 명세서
아래 주소로 접속하면 API 명세서가 생성됨
> Swagger UI : http://localhost:8000/docs

> ReDoc : http://localhost:8000/redoc

## curl 명령어 (api-test01 기반 예시)
터미널에서 직접 실행할 수 있다.
### get
```
curl <주소>
```
### post
```
curl -X POST http://127.0.0.1:8000/items \
-H "Content-Type: application/json" \
-d '{
    "name":"MacBook Pro",
    "price":3200000,
    "stock":10,
    "description":"M4 Pro"
}'
```
### put
```
curl -X PUT http://127.0.0.1:8000/items/1 \
-H "Content-Type: application/json" \
-d '{
    "name":"iPhone",
    "price":1800000,
    "stock":20,
    "description":"iPhone 17"
}'
```
### patch
```
curl -X PATCH "http://127.0.0.1:8000/items/1?description=새로운설명"
```
### delete
```
curl -X DELETE http://127.0.0.1:8000/items/1
```

## 백엔드와 프론트엔드 연결
포트가 다르면 CORS 에러 발생
