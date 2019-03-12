# docker-compose-anemometer

## Usage

1. `docker-compose up -d`

2. Go to `http://localhost:10080`

3. Put some data in the DB

  ```bash
  $ cat slow.log | docker-compose run pt pt-query-digest \
                     --user=anemometer --password=superSecurePass \
                     --review h=mysql56,D=slow_query_log,t=global_query_review \
                     --history h=mysql56,D=slow_query_log,t=global_query_review_history \
                     --no-report --limit=0% \
                     --filter=" \$event->{Bytes} = length(\$event->{arg}) and \$event->{hostname}=\"HOSTNAME\""
  ```
