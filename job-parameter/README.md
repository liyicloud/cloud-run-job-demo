# Cloud Run Jobsの実践
https://qiita.com/sugarperson/items/95cf60dec7511928104e

## Artifact Registryの作成
gcloud artifacts repositories create sample-repo \
--repository-format=docker \
--location=asia-northeast1 \
--description="Cloud Run Sample Repository" \
--project="cloud-run-drill"


### イメージをビルド
docker build -t run-job-param .

### イメージをタグ付け
docker tag run-job-param:latest asia-northeast1-docker.pkg.dev/cloud-run-drill/sample-repo/run-job-param:latest

### イメージをプッシュ
docker push asia-northeast1-docker.pkg.dev/cloud-run-drill/sample-repo/run-job-param:latest



## ジョブを作成
gcloud run jobs create run-job-param \
--image asia-northeast1-docker.pkg.dev/cloud-run-drill/sample-repo/run-job-param:latest \
--region=asia-northeast1 \
--tasks=1 \
--cpu=1 \
--max-retries=0 \
--memory=512Mi \
--parallelism=1 \
--task-timeout=100

## ジョブを実行
gcloud run jobs execute run-job-param --region=asia-northeast1

## コマンド引数を与えて実行
gcloud run jobs execute run-job-param --region=asia-northeast1 --args="arg1,arg2,arg3"

