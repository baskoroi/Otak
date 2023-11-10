#permanent #okhome #okhome-api #performance

1. caching redundant responses
2. separate read query (use replica DB) from write queries (use master DB)
3. multithreading -> for heavy processes
4. periodically check for anomalies/errors in Kibana logging
	1. make hotfix for each anomaly / error / slowdonw / repetitive logging
	2. you can learn okhome-api flow through logs
 5. check heavy DB queries -> optimize/tune them
 6. check for scheduler jobs with intense processing, or the unsuccessful ones but executed with very high execution count
 7. reactive? no thanks. need to implement till FE level, else in vain.