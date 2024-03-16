# GCP serverless and integration with pubsub

## Topic creation in Pub/Sub

```sh
# gcloud pubsub topics create <TOPIC_NAME> --message-retention-duration=1h
$ gcloud pubsub topics create help_call --message-retention-duration=1h
```