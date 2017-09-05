# bigdump
Helps in importing big database dump (Copy of http://www.ozerov.de/bigdump/)


# Usage
Download and unzip bigdump.zip on your PC.
Open bigdump.php in a text editor, adjust the database configuration and dump file encoding.
Drop the old tables on the target database if your dump doesn’t contain “DROP TABLE” (use phpMyAdmin).
Create the working directory (e.g. dump) on your web server
Upload bigdump.php and the dump files (*.sql or *.gz) via FTP to the working directory (take care of TEXT mode upload for bigdump.php and dump.sql but BINARY mode for dump.gz if uploading from MS Windows).
Run the bigdump.php from your web browser via URL like http://www.yourdomain.com/dump/bigdump.php.
Now you can select the file to be imported from the listing of your working directory. Click “Start import” to start.
BigDump will start every next import session automatically if JavaScript is enabled in your browser.
Relax and wait for the script to finish. Do NOT close the browser window!
IMPORTANT: Remove bigdump.php and your dump files from your web server.


# Advanced notes

Note 1: BigDump will fail processing large tables containing extended inserts. An extended insert contains all table entries within one SQL query. BigDump isn’t able to split such SQL queries. In most cases BigDump will stop if some query includes to many lines. But if PHP complains that allowed memory size exhausted or MySQL server has gone away your dump probably also contains extended inserts. Please turn off extended inserts when exporting database from phpMyAdmin. If you only have a dump file with extended inserts please ask for our support service in order to convert it into a file usable by BigDump.

Note 2: If you want to upload the dump files via web browser give the scripts writing permissions on the working directory (e.g. make chmod 777 on a Linux based system). You can upload the dump files from the browser up to the size limit set by the current PHP configuration of the web server. Alternatively you can upload any files via FTP. Some web servers disallow script execution in the directory with writing permissions for security reasons. If you changed the permissions on the working directory and you are getting a server error when running the script restore the permissions to their normal state (chmod 755) for directories.

Note 3: If Timeout errors still occur you may need to adjust the $linespersession setting in bigdump.php.

Note 4: If mySQL server overrun occurs due to max_requests restriction you can use $delaypersession setting to let the script sleep some milliseconds or more before starting next session. This setting will only work if the JavaScript is activated. Importing dump file on such servers may be very time consuming.

Note 5: BigDump is currently not able to restore a single dump file with multiple databases inside (switched by the USE statement). BigDump is also not able to restore a single specific database from the dump file containing multiple databases.

Note 6: If you experience problems with non-latin characters while using BigDump you have to adjust the $db_connection_char_set configuration variable in bigdump.php to match the encoding of your dump file.

Note 7: GZip support is only available with PHP 4.3.0 and later. Using a huge GZip compressed dump file can cause the script to exceed the PHP memory/runtime limit since the dump file has to be unpacked from the beginning every time the session starts. If this happens use the uncompressed dump. It’s your only chance.

Note 8: It’s not a very good idea, but if you can also import from CSV file into one mySQL table using Bigdump. You have to specify the table name in $csv_insert_table. Please also check other CSV settings in the Bigdump configuration.