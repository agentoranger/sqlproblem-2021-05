For those who end up here, this issue is somewhat deprecated.  Please refer the following reddit thread for the answers.

https://www.reddit.com/r/PostgreSQL/comments/n5ln31/function_performs_very_slowly_when_used_for_the/

Function performs very slowly when used for the 6th time
Hey there, My name is a Brian and I am a sysadmin for a small company here in pittsburgh. I am looking what I consider to be a very curious problem. If you are looking for a brain teaser, look no further. I found that resolving this issue on my own is well above my capacity.

Our dba put together a rather complex function that generally performs well. However, when the function is performed more than 5 times in a single user session (psql, pgadmin, erp) the function begins to slow down drastically on the 6th execution and will perform that way until we log off of the session. Starting a new session will allow the function to perform quickly again.

This occurs when using PostgreSQL v10 and PostgreSQL v11.

Pg10 Server Parameters
Ubuntu 18.04.5 LTS
PostgreSQL 10.16-1.pgdg18.04+1
CPU: 16 cores 8 threads
MEM: 42GB
31GB effective cache
11GB shared buffers on 1GB large pages
512MB temp buffers
68812kB work_mem

Pg11 Server Parameters
Ubuntu 20.04.5 LTS
PostgreSQL 11.11-1.pgdg20.04+1
CPU: 16 cores 8 threads
MEM: 42GB
31GB effective cache
11GB shared buffers on 1GB large pages
512MB temp buffers
68812kB work_mem

Here are the non standard parameters we have set in postgresql.conf
postgresql.conf

Sample of timing the function 5 and 6 times in the same session illustrates the slowdown.

r/PostgreSQL - Function performs very slowly when used for the 6th time
Here is a copy of the complete function:
network_search_1_function.txt

Here is the statement I used to test the function:
network_search_1_testing_statment.txt

Here is a general query plan for the 2nd execution of the function.
queryplan_2nd_execution.txt

Here is a general query plan for the 6th execution of the function (slowdown).
queryplan_6th_execution.txt

Here is a fully explained query plan using auto_explain to extract the full details. This is showing both the 5th (fast) and 6th (slow) executions.
https://github.com/agentoranger/sqlproblem-2021-05/blob/main/detailed-explain-slowdown.txt
