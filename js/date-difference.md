Subtracting one date from another will give you the difference in MS. You can then break that down to the granularity you need.

```
d1 = new Date("2019-05-01");
d2 = new Date("2020-05-05");

msDiff = d2 - d1;
secDiff = msDiff / 1000;
minDiff = secDiff / 60;
hourDiff = minDiff / 60;
dayDiff = hourDiff / 24;
```
