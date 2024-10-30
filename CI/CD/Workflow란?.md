# < GIthub Action Workflow >

### Workflow란?
- 자동화 작업의 가장 상위 개념으로, 하나 이상의 작업(Job)을 실행시키는 자동화 구성
- GitHub 레포지토리 내 .github/workflows라는 디렉토리에 YAML 파일 단위로 정의
- GitHub 레포지토리에서 발생되는 이벤트 (ex. 코드 푸시, 이슈 생성)가 발생할 때 자동으로 실행

### Workflow 구성 예시
```
name: PART3 - CH3 - Job Basic Sample # 워크플로우의 이름. UI상 워크 플로우 이름을 표시하게 됨
on: workflow_dispatch # 워크플로우 실행을 위한 트리거 정의. workflow_dispatch는 사용자에 의한 수동 트리거
jobs: # 워크플로우에서 실행하고자 하는 작업에 대한 정의. 하나 이상의 작업(job)으로 구성. 각 작업(job)은 별도의 실행기(Runner)로 구성
  build:
    name: Build and Test
    runs-on: ubuntu-latest
    steps:
    - name: Checkout 
      uses: actions/checkout@v2
    - name: Build project
      run: |
        echo "Build Project"
    - name: Run tests
      run: |
        echo "Run Test"
  deploy:
    name: Deploy to production
    needs: build
    runs-on: ubuntu-latest
    steps:
    - name: Deploy to production
      run: |
        echo "Deploying to production server"
```

20241030