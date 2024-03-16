# GCP serverless and integration with pubsub

## Topic creation in Pub/Sub

```sh
# gcloud pubsub topics create <TOPIC_NAME> --message-retention-duration=1h
$ gcloud pubsub topics create help_call --message-retention-duration=1h
```

```sh
# gcloud functions deploy <FUNCTION_NAME> --entry-point liga --runtime python39 --trigger-topic <TOPIC> --allow-unauthenticated --memory 128MB --region us-central1
$ gcloud functions deploy function-public-citizen-http --entry-point liga --runtime python39 --trigger-topic call_help --allow-unauthenticated --memory 128MB --region us-central1 -
```