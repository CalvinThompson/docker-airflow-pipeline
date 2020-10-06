# Data Pipeline with Docker and Airflow
## Loading from AWS S3 to AWS Redshift

The main goal of this project is to transform raw event and log data stored in json files on AWS S3 into an analytics ready data model on AWS Redshift.

### Data Pipeline
![DAG](./data-pipeline-dag.png)

## Data Model
![model](./data-model.png)

### Installing
1. Install [Docker](https://www.docker.com/get-started).

2. Set up AWS:
    1. Create an [AWS account](https://aws.amazon.com/premiumsupport/knowledge-center/create-and-activate-aws-account/)
    2. Generate [AWS access keys](https://docs.aws.amazon.com/general/latest/gr/aws-sec-cred-types.html)
    3. Launch a [Redshift Cluster](https://docs.aws.amazon.com/redshift/latest/gsg/rs-gsg-launch-sample-cluster.html) and enable public access


3. Start the **docker container**.
    ```
    docker-compose up -d
    ```

4. After a few moments the Airflow webserver will start, connect to it at http://localhost:8080/admin/

    Use Airflow UI to set up connections to AWS Account and AWS Redshift

    1. Go to Airflow UI Admin/Connections and navigate to the Create tab.
    ![AirFlow Admin Panel](./airflow-UI.png)

    2. Set up connection to AWS Account:
      * **Conn Id**: Enter `aws_credentials`.
      * **Conn Type**: Select `Amazon Web Services`.
      * **Login**: Enter your **Access key ID** from the IAM User credentials you downloaded.
      * **Password**: Enter your **Secret access key** from the IAM User credentials you downloaded.

    3. Set up connection to AWS Redshift:
      * **Conn Id**: Enter `redshift`.
      * **Conn Type**: Enter `Postgres`.
      * **Host**: Enter your AWS Redshift endpoint.
      * **Schema**: Enter `dev`.
      * **Login**: Enter your AWS Redshift master user name.
      * **Password**: Enter your AWS Redshift master user password.
      * **Port**: Enter `5439`

### Run the DAG
1. Navigate to DAGs and switch on the sparkify_pipeline DAG
