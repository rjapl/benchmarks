1. download source data:
```
curl -s https://s3.amazonaws.com/nyc-tlc/trip+data/yellow_tripdata_2017-01.csv > 2017.01
```
2. process downloaded data:
```
gawk 'NR>2{print(gensub(/(-[0-9]{2}) ([0-9]{2}:)/, "\\1T\\2","g"));}' 2017.01 > 2017.01.csv
```
3. run XDB:
```
xdb 0.x
```
4. 5.3ns/row for full table scan(Intel(R) Core(TM) i7-7700T CPU @ 2.90GHz/16GB memory/HDD):
```
 \t select from t1m where total_amount=max total_amount
51
```
