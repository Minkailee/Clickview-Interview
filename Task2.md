## We have a variant column in a Snowflake database that we use to store semi-structured data in JSON format. The structure of the data looks like this:
    {
        "id": 1,
        "folders": [
            {
                "id": 10,
                "name": "History"
            },
            {
                "id": 11,
                "name":"Science"
            }
        ],
        "libraries": [
            {
                "id": 12,
                "name": "Primary AU"
            },
            {
                "id": 13,
                "name": "Secondary AU"
            }
        ],
        "series": {
                "id": 14,
                "name": "Einstein"
            }
    }
## Write the following Snowflake SQL queries that will return all the rows in the table that:
### a) Have a folder id of 10
    create or replace table task2 (v variant);
    insert into task2
        select
        parse_json(
        '{
            "id": 1,
            "folders": [
                {
                    "id": 10,
                    "name": "History"
                },
                {
                    "id": 11,
                    "name":"Science"
                }
            ],
            "libraries": [
                {
                    "id": 12,
                    "name": "Primary AU"
                },
                {
                    "id": 13,
                    "name": "Secondary AU"
                }
            ],
            "series": {
                    "id": 14,
                    "name": "Einstein"
                }
        }');
    SELECT
        v:id::int as id,
        f1.value:id::int as folder_id,
        f1.value:name::string as folder_name,
        f2.value:id::int as library_id,
        f2.value:name:: string as library_name,
        v:series:id::int as series_id,
        v:seires:name::string as seires_name
    FROM
        task2,
        table(flatten(v:folders)) f1,
        table(flatten(v:libraries)) f2
    WHERE
        folder_id = 10
    ;
        
### b) Have a library Id of 12 and a series Id of 14
    SELECT
        v:id::int as id,
        f1.value:id::int as folder_id,
        f1.value:name::string as folder_name,
        f2.value:id::int as library_id,
        f2.value:name:: string as library_name,
        v:series:id::int as series_id,
        v:seires:name::string as seires_name
    FROM
        task2,
        table(flatten(v:folders)) f1,
        table(flatten(v:libraries)) f2
    WHERE
        library_id = 12
    AND
        series_id = 14
    ;