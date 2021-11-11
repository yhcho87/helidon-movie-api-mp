# OKE HandsOn

### ocicli 설치 및 설정
설치
> https://thekoguryo.github.io/oci/chapter14/1/1/1/

설정
> https://thekoguryo.github.io/oci/chapter14/1/1/3/

### kubectl 설치
> https://kubernetes.io/ko/docs/tasks/tools/install-kubectl-windows/

### ocicli 설치 및 kubectl 설치 없이 Cloud Shell을 활용
우측 상단의 Cloud Shell 버튼 클릭한 후 오픈된 Cloud Shell에서 실습 진행

### OKE 클러스터 생성
1. OCI Console 접속 후 "우측 상단 햄버거 버튼 클릭 > Developer Services > Kubernetes Cluster" 선택
2. "Create Cluster > Quick Create" 선택
3. Cluster 이름 입력 (e.g. oke-cluster1)
4. 앞서 생성한 Compartment 선택
5. Shape: VM.Standard2.1 선택
6. Next 선택 후 생성

### KUBECONFIG 생성
1. 생성된 클러스터를 클릭한 후 Access Cluster 버튼을 선택
2. 오픈된 팝업창의 가이드 순서대로 진행

### kubectl 테스트
```
$ kubectl get nodes
```

### 샘플 애플리케이션
> https://github.com/MangDan/helidon-movie-api-mp

**소스 다운로드**
```
$ git clone https://github.com/MangDan/helidon-movie-api-mp
```

### 이미지 빌드 및 푸시
**이미지 태그 형태**
> {리전코드}.ocir.io/{오브젝트 스토리지 네임스페이스}/{레파지토리명}/{이미지명}:{태그}

```
$ docker build -t icn.ocir.io/idxikmibcwcd/movie/helidon-movie-api-mp:1.0 .
$ docker push icn.ocir.io/idxikmibcwcd/movie/helidon-movie-api-mp:1.0
```

### Deploy
$ kubectl apply -f kube-helidon-movie-api-mp-config-direct.yml
