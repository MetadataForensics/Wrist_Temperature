# Wrist Temperature
Our SQL query for Wrist Temperature data recorded by the Apple Watch while the user is sleeping. Results from this query mirror that of what the user would see within Health Application > Show All Health Data > Wrist Temperature > Show All Data. Here, each days data is parsed to mirror the sample and device details. This data can lend insight into the well-being of the user, [Apple](https://support.apple.com/en-us/102674) cites variables to Wrist Temperature such as diet, exercise, alcohol consumption, menstrual cycles, and illness.

# Where to Use:

- The SQL queries will work in most SQLite database viewers able to execute SQL queries. 
- Supported within iLEAPP, available [here](https://github.com/abrignoni/iLEAPP).

# File Location
This data pertains to the Apple Watch and recorded within the healthdb_secure.sqlite and health.sqlite databases, available through encrypted Advanced Logical and Full File System Extractions. As the SQL query pulls data from both databases, the health.sqlite database must be attached with database name healthdb prior to running the query - this can be completed within DB Browser for SQLite and other database viewers.

# More Details
According to [Apple](https://support.apple.com/en-us/102674), any model of the Apple Watch Ultra, Watch Series 8, or Watch Series newer than the 8 is needed; Sleep must be set up with Track Sleep; and Sleep Focus must be enabled for at least 4 hours nightly for about 5 nights. 

The data_type for Wrist Temperature is 256 - used within our WHERE clause to narrow our results just to Wrist Temperature.

Somewhat uniquely, this query also uses Common Table Expressions (CTEs), which are required to obtain both the Algorithm Version and Skin Surface Temperature data. The WITH keyword allows us to define CTEs to use within our main query. Looking at the data: 

<img width="1180" height="122" alt="Screenshot 2025-07-16 142456" src="https://github.com/user-attachments/assets/6f6c8931-2f26-4d87-aa53-919944f965cf" />
 
Filtering our **samples** table for data_type 256 provides data_id values as well as start_date and end_date timestamps. Further filtering our **metadata_values** table object_id column with a data_id value from the **samples** table reveals two rows of data. The **metadata_keys** table joins to the **metadata_values** table through metadata_values.key_id = metadata_keys.ROWID. The metadata_keys.key value yields the context behind our metadata_values.numerical_value data. Note: As the metadata_keys.key value to ROWID value can vary our query uses the key value.

# Resources referenced:
-  [DB Browser for SQLite](https://sqlitebrowser.org/) (Image above is a depiction through DB Browser for SQLite, Version 3.13.1)
-  [iLEAPP](https://github.com/abrignoni/iLEAPP)
