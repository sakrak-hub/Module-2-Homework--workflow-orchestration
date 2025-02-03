Question 1)
Within the execution for Yellow Taxi data for the year 2020 and month 12: what is the uncompressed file size (i.e. the output file yellow_tripdata_2020-12.csv of the extract task)?

Ans: 

id: kestra-postgres
namespace: zoomcamp

inputs:
  - id: taxi
    type: SELECT
    displayName: Select taxi type
    values: [yellow, green]
    defaults: yellow

  - id: year
    type: SELECT
    displayName: Select year
    values: ["2019", "2020"]
    defaults: "2019"

  - id: month
    type: SELECT
    displayName: Select month
    values: ["01", "02", "03", "04", "05", "06", "07", "08", "09", "10", "11", "12"]
    defaults: "01"

tasks:
  - id: set_label
    type: io.kestra.plugin.core.execution.Labels
    labels:
      file: "{{render(vars.file)}}"
      taxi: "{{inputs.taxi}}"

  - id: extract
    type: io.kestra.plugin.scripts.shell.Commands
    outputFiles:
      - "*.csv"
    taskRunner:
      type: io.kestra.plugin.core.runner.Process
    commands:
      - wget -qO- https://github.com/DataTalksClub/nyc-tlc-data/releases/download/{{inputs.taxi}}/{{render(vars.file)}}.gz | gunzip > {{render(vars.file)}}

--------------------------------------------------------------------------------------------------------------------------------
Question 3)
How many rows are there for the Yellow Taxi data for all CSV files in the year 2020?

SELECT COUNT(*) FROM yellow_tripdata WHERE filename LIKE '%2020%'
--------------------------------------------------------------------------------------------------------------------------------
Question 4)
How many rows are there for the Green Taxi data for all CSV files in the year 2020?

SELECT COUNT(*) FROM yellow_tripdata WHERE filename LIKE '%2020%'
--------------------------------------------------------------------------------------------------------------------------------
Question 5)
How many rows are there for the Yellow Taxi data for the March 2021 CSV file?

SELECT COUNT(*) FROM yellow_tripdata WHERE filename LIKE '%2021-03.csv'