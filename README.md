# mysql-dnxcore50
This is a barely-tested, stripped-down version of the MySQL Connector/Net 6.9.7 library for DNXCore50.

I've removed tons of Windows-specific functionality, replication, localization, transactions, etc. The following basic scenario works:

```
   string connectionString = "server=127.0.0.1;userid=my_user;password=my_password;database=my_db;default command timeout=10;Connection Timeout=5;";

	using (var conn = new MySqlConnection(connectionString))
	{
		conn.Open();
		var cmd = new MySqlCommand(@"select col1, col2 from data where id = @id", conn);
		cmd.Parameters.AddWithValue("@id", "myId");
		var reader = cmd.ExecuteReader();
		
		string col1data;
		string col2data;
		
		if (reader.Read())
		{
	
			if (!reader.IsDBNull(0))
			{
				col1data = reader.GetString(0);
			}

			if (!reader.IsDBNull(1))
			{
				col2data = reader.GetString(1);
			}
		}
	}
```
