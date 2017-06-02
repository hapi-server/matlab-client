For binary it is a significant fraction of time. Based on testing with MATLAB, if we used doubles for time, the time to have data in a form for plotting is ~75x faster. Typical results for (a benchmark script)[https://github.com/hapi-server/matlab-client)[https://github.com/hapi-server/matlab-client/binary_compare.m] are:

```
fbin total time:       0.0336
bin memmap time:       0.0025
bin extract data time: 0.1569
bin extract time time: 0.0897
bin datenum time:      1.4137
```

This corresponds to a speed-up of 74 = (1.41 + 0.9 + 0.16 + 0.0025)/0.0336 (this varies between 25 and 300 on my machine).

Therefore our specification for binary somewhat defeats the purpose of binary (speed). We could either define a new binary output (e.g., "sensiblebinary") or modify the existing.

Suggestion for modification of existing binary or new "sensiblebinary" output option: 

Specify in the first 22 bytes in the binary response as: Byte 1 (char) = 0-3 corresponding to (seconds, milli, micro, nano), Bytes 2-22 (chars) = yyyy-mm-ddTHH:MM:SS + \0.  Possibly we should have bytes 23-100 be reserved for future use.

Sensible binary has been implemented in (https://github.com/hapi-server/matlab-client)[https://github.com/hapi-server/matlab-client] and (https://github.com/hapi-server/python-client)[https://github.com/hapi-server/python-client].