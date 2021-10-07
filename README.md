# thread-dump-compare
Compare multiple thread dumps in a directory based on ThreadName and State

Sample thread dumps are provided in the tmp directory.

STEPS DONE IN THE CODE
----------------------
A Single Thread dump line like looks like this:
"HttpClient@58df7f61-496" #496 prio=5 os_prio=31 cpu=0.25ms elapsed=9.55s tid=0x00007fe0bb61b000 nid=0x2927b waiting on condition  [0x000070000a17e000]

Here we are first extraction the Thread Name and its state and putting them inside a dataframe:
"HttpClient@58df7f61-496",waiting on condition

We do this for all files in the provided directory, so at the end, we have multiple dataframes each with Dataframe for a file in the directory.
For E.g.
tmp/td1, tmp/td2 and tmp/td3 will have 1 dataframe each containing the above information.

We then try to remove threadnumber identification inside the Thread Name.
For this we take the string before the "-" symbol"
HttpClient@58df7f61-496 ==> HttpClient@58df7f61

(Note that this is not a full proof method since ThreadNames can have other characters like # etc that are used in place of "-" used before the number. in those cases, you will have to add additional code to extract that information)

We can also add other informations in the regular expression like cpu/elapsed etc. This can be used for other analysis.
