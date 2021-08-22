# a) Please explain the following with an example of when would be a good time to you it:
## Inner Join:
### Explanation: 
Take the records of the two tabels that fullfill the same join conditions and combine the required columns.
### Example: 
With Table1(Products selling in shop1) and Tbale2(Products selling in shop2), find out the products selling in both shop. 
### SQL: 
    SELECT 
        TABLE1.PRODUCT_ID 
    FROM 
        TABLE1 
    INNER JOIN 
        TABLE2 
    ON 
        TABLE1.PRODUCT_ID = TABLE2.PRODUCT_ID
    ;

## Full Outer Join:
### Explanation: 
Take all the records from the two tables and combined the required columns.
### Example: 
With Table1(Products selling in shop1) and Tbale2(Products selling in shop2), find out the products that are selling in either shop1 or shop2. 
### SQL: 
    SELECT 
        COALESCE(TABLE1.PRODUCT_ID, TABLE2.PRODUCT_ID) AS PRODUCT_ID 
    FROM 
        TABLE1 
    OUTER 
        JOIN TABLE2 
    ON 
        TABLE1.PRODUCT_ID = TABLE2.PRODUCT_ID
    ;
## Left Join:
### Explanation: 
Take all the records from the left tables and the records that fullfill the join conditions from the right table.
### Example: 
With Table1(Products selling in shop1) and Tbale2(Products selling in shop2), find out whether the products selling in shop1 are also selling in shop2. 
### SQL: 
    SELECT 
        TABLE1.PRODUCT_ID, 
        CASE 
            WHEN TABLE2.PRODUCT_ID IS NOT NULL 
            THEN 'Yes' 
            ELSE 'No' 
            END AS Selling_in_Shop2 
        FROM 
            TABLE1 LEFT JOIN TABLE2 
        ON 
            TABLE1.PRODUCT_ID = TABLE2.PRODUCT_ID
        ;
## Right Join:
### Explanation: 
Take all the records from the right tables and the records that fullfill the join conditions from the left table.
### Example: 
With Table1(Products selling in shop1) and Tbale2(Products selling in shop2), find out whether the products selling in shop2 are also selling in shop1.
### SQL: 
    SELECT 
        TABLE2.PRODUCT_ID, 
        CASE 
            WHEN TABLE1.PRODUCT_ID IS NOT NULL 
            THEN 'Yes' 
            ELSE 'No' 
            END AS Selling_in_Shop1 
        FROM 
            TABLE1 RIGHT JOIN TABLE2 
        ON 
            TABLE1.PRODUCT_ID = TABLE2.PRODUCT_ID
    ;
## Cross join:
### Explanation: 
Take all the possible paired combination of each record of the left table with each record of the right table. 
### Example: 
With Table1(Products selling in shop1) and Tbale2(Products selling in shop2), find out all the possible products combinations if someone randomly buy one product form each shop respectivly. 
### SQL: 
    SELECT 
        TABLE1.PRODUCT_ID AS SHOP1_PRODUCT, 
        TABLE2.PRODUCT_ID AS SHOP2_PRODUCT
    FROM 
        TABLE1 CROSS JOIN TABLE2 
    ON 
        TABLE1.PRODUCT_ID = TABLE2.PRODUCT_ID
    ;


# b) Please explain how natural joins differ from explicit joins
### Explanation: 
Natural Join gives you the records from the two tables that sharing the common columns, but explicit join would only give you the records that fullfill the join conditions.