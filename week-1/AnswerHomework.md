1. Google Cloud SDK 368.0.0
2. var.project
  Your GCP Project ID

  Enter a value: data-enginering-zoomcamp


Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the
following symbols:
  + create

Terraform will perform the following actions:

  # google_bigquery_dataset.dataset will be created
  + resource "google_bigquery_dataset" "dataset" {
      + creation_time              = (known after apply)
      + dataset_id                 = "trips_data_all"
      + delete_contents_on_destroy = false
      + etag                       = (known after apply)
      + id                         = (known after apply)
      + last_modified_time         = (known after apply)
      + location                   = "europe-west6"
      + project                    = "data-enginering-zoomcamp"
      + self_link                  = (known after apply)

      + access {
          + domain         = (known after apply)
          + group_by_email = (known after apply)
          + role           = (known after apply)
          + special_group  = (known after apply)
          + user_by_email  = (known after apply)

          + view {
              + dataset_id = (known after apply)
              + project_id = (known after apply)
              + table_id   = (known after apply)
            }
        }
    }

  # google_storage_bucket.data-lake-bucket will be created
  + resource "google_storage_bucket" "data-lake-bucket" {
      + force_destroy               = true
      + id                          = (known after apply)
      + location                    = "EUROPE-WEST6"
      + name                        = "dtc_data_lake_data-enginering-zoomcamp"
      + project                     = (known after apply)
      + self_link                   = (known after apply)
      + storage_class               = "STANDARD"
      + uniform_bucket_level_access = true
      + url                         = (known after apply)

      + lifecycle_rule {
          + action {
              + type = "Delete"
            }

          + condition {
              + age                   = 30
              + matches_storage_class = []
              + with_state            = (known after apply)
            }
        }

      + versioning {
          + enabled = true
        }
    }

Plan: 2 to add, 0 to change, 0 to destroy.

Do you want to perform these actions?
  Terraform will perform the actions described above.
  Only 'yes' will be accepted to approve.

  Enter a value: yes

google_bigquery_dataset.dataset: Creating...
google_storage_bucket.data-lake-bucket: Creating...
google_storage_bucket.data-lake-bucket: Creation complete after 3s [id=dtc_data_lake_data-enginering-zoomcamp]
google_bigquery_dataset.dataset: Creation complete after 3s [id=projects/data-enginering-zoomcamp/datasets/trips_data_all]

Apply complete! Resources: 2 added, 0 changed, 0 destroyed.

3. 53024
SELECT COUNT(tpep_pickup_datetime)
FROM yellow_taxi_data
WHERE tpep_pickup_datetime >= to_timestamp('15-01-2021 00:00:00', 'dd-mm-yyyy hh24:mi:ss')
  and tpep_pickup_datetime <= to_timestamp('15-01-2021 23:59:59', 'dd-mm-yyyy hh24:mi:ss')

4. Wednesday --> 2021-01-20 11:22:05
SELECT *
FROM yellow_taxi_data
WHERE tip_amount = 1140.44

5.  237 --> Upper East Side South
SELECT "DOLocationID", COUNT("DOLocationID")
FROM yellow_taxi_data
WHERE tpep_pickup_datetime >= to_timestamp('14-01-2021 00:00:00', 'dd-mm-yyyy hh24:mi:ss')
  and tpep_pickup_datetime <= to_timestamp('14-01-2021 23:59:59', 'dd-mm-yyyy hh24:mi:ss')
  and "PULocationID" = 43
GROUP BY "DOLocationID"
HAVING COUNT("DOLocationID")>1
ORDER BY count DESC

6. 140 --> Lenox Hill East 236 --> Upper East Side North
select *
from yellow_taxi_data
where Total_amount = 7661.28
