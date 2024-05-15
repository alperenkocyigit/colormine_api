
<div class="cell markdown" id="XdSucRD2frYb">

# Colormine CIE2000 LCH Color Compare Using API

</div>

<div class="cell markdown">

Enter some LCH color values to calculate the CIE DE2000 (aka DE2000 or
CIE2000) score. Note: This calculation is Quasimetric, the result may
vary based on which value you enter first!

</div>

<div class="cell markdown" id="7EYRzKtDf12L">

Example Curl Request

</div>

<div class="cell code" execution_count="1" id="H-OPwGtAlqOf">

``` python
!curl 'http://colormine.org/api/Cie2000/Compare?request=\{%22A%22:\{%22Type%22:%22Lch%22,%22L%22:%2211.1%22,%22C%22:%2222.2%22,%22H%22:%2233.3%22\},%22B%22:\{%22Type%22:%22Lch%22,%22L%22:%2244.4%22,%22C%22:%2255.5%22,%22H%22:%2266.6%22\}\}' \
  -H 'Accept: */*' \
  -H 'Accept-Language: en-US,en;q=0.9' \
  -H 'Connection: keep-alive' \
  -H 'Referer: http://colormine.org/delta-e-calculator/cie2000' \
  -H 'User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/123.0.0.0 Safari/537.36 OPR/109.0.0.0' \
  -H 'X-Requested-With: XMLHttpRequest' \
  --insecure
```

<div class="output stream stdout">

    14.9191

</div>

</div>

<div class="cell markdown">

## Example usage for 1 compare

</div>

<div class="cell code" execution_count="9">

``` python
import requests

# Decarling the variables

# First color's LCH values
L1 = "11.1"
C1 = "12.1" 
H1 = "13.1"

# Second color's LCH values
L2 = "14.1"
C2 = "15.1"
H2 = "16.1"

# Create the dynamic URL structure for LCH value comparison
url = "http://colormine.org/api/Cie2000/Compare?request={{%22A%22:{{%22Type%22:%22Lch%22,%22L%22:%22{}%22,%22C%22:%22{}%22,%22H%22:%22{}%22}},%22B%22:{{%22Type%22:%22Lch%22,%22L%22:%22{}%22,%22C%22:%22{}%22,%22H%22:%22{}%22}}}}"
url = url.format(L1, C1, H1, L2, C2, H2)

# Set the headers
headers = {
    'Accept': '*/*',
    'Accept-Language': 'en-US,en;q=0.9',
    'Connection': 'keep-alive',
    'Referer': 'http://colormine.org/delta-e-calculator/cie2000',
    'User-Agent': 'Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/123.0.0.0 Safari/537.36 OPR/109.0.0.0',
    'X-Requested-With': 'XMLHttpRequest'
}
```

</div>

<div class="cell code" execution_count="10">

``` python
# Make the request
response = requests.get(url, headers=headers, verify=False)

# Check if the request was successful
if response.status_code == 200:
    print(response.text)
else:
    print("Request failed with status code: {}".format(response.status_code))
```

<div class="output stream stdout">

    2.8034

</div>

</div>

<div class="cell markdown">

## Example usage for multi compare from manual input

</div>

<div class="cell code" execution_count="11">

``` python
import requests

# Declare the variable lists
L1_values = ["11.1", "22.2", "33.3", "44.4", "55.5", "66.6", "77.7", "88.8", "99.9", "10.1"]
C1_values = ["12.1", "23.2", "34.3", "45.4", "56.5", "67.6", "78.7", "89.8", "90.9", "11.1"]
H1_values = ["13.1", "24.2", "35.3", "46.4", "57.5", "68.6", "79.7", "80.8", "91.9", "12.1"]
L2_values = ["14.1", "25.2", "36.3", "47.4", "58.5", "69.6", "70.7", "81.8", "92.9", "13.1"]
C2_values = ["15.1", "26.2", "37.3", "48.4", "59.5", "60.6", "71.7", "82.8", "93.9", "14.1"]
H2_values = ["16.1", "27.2", "38.3", "49.4", "50.5", "61.6", "72.7", "83.8", "94.9", "15.1"]

# Create the dynamic URL structure for LCH value comparison
url_template = "http://colormine.org/api/Cie2000/Compare?request={{%22A%22:{{%22Type%22:%22Lch%22,%22L%22:%22{}%22,%22C%22:%22{}%22,%22H%22:%22{}%22}},%22B%22:{{%22Type%22:%22Lch%22,%22L%22:%22{}%22,%22C%22:%22{}%22,%22H%22:%22{}%22}}}}"

# Set the headers
headers = {
    'Accept': '*/*',
    'Accept-Language': 'en-US,en;q=0.9',
    'Connection': 'keep-alive',
    'Referer': 'http://colormine.org/delta-e-calculator/cie2000',
    'User-Agent': 'Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/123.0.0.0 Safari/537.36 OPR/109.0.0.0',
    'X-Requested-With': 'XMLHttpRequest'
}
```

</div>

<div class="cell code" execution_count="12">

``` python
# Make the requests for each color pair
for i in range(10):
    url = url_template.format(L1_values[i], C1_values[i], H1_values[i], L2_values[i], C2_values[i], H2_values[i])
    response = requests.get(url, headers=headers, verify=False)
    
    if response.status_code == 200:
        print(f"Response {i+1}: {response.text}")
    else:
        print(f"Response {i+1} failed with status code: {response.status_code}")
```

<div class="output stream stdout">

    Response 1: 2.8034
    Response 2: 1.7419
    Response 3: 2.1387
    Response 4: 1.7056
    Response 5: 5.56
    Response 6: 9.018
    Response 7: NaN
    Response 8: 3.0119
    Response 9: 5.9041
    Response 10: 2.8225

</div>

</div>

<div class="cell markdown">

## Example usage for multi compare from csv input

</div>

<div class="cell code" execution_count="20">

``` python
import requests
import csv

# Read the dataset
with open('dataset.csv', 'r') as file:
    reader = csv.reader(file, delimiter=';')
    data = list(reader)

# Split the data into two groups(First is control group, second is test group)
group1 = data[:10]
group2 = data[10:20]

# Visualize the data
print(data[:10])

# Create the dynamic URL structure for LCH value comparison
url_template = "http://colormine.org/api/Cie2000/Compare?request={{%22A%22:{{%22Type%22:%22Lch%22,%22L%22:%22{}%22,%22C%22:%22{}%22,%22H%22:%22{}%22}},%22B%22:{{%22Type%22:%22Lch%22,%22L%22:%22{}%22,%22C%22:%22{}%22,%22H%22:%22{}%22}}}}"

# Set the headers
headers = {
    'Accept': '*/*',
    'Accept-Language': 'en-US,en;q=0.9',
    'Connection': 'keep-alive',
    'Referer': 'http://colormine.org/delta-e-calculator/cie2000',
    'User-Agent': 'Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/123.0.0.0 Safari/537.36 OPR/109.0.0.0',
    'X-Requested-With': 'XMLHttpRequest'
}
```

<div class="output stream stdout">

    [['0,70', '0,37', '2,20', '0,23', '1,50', '1,20', '0,93', '0,53', '0,37', '0,20', '0,27', '1,73', '0,17', '1,30', '0,93', '0,20', '1,33', '1,07', '0,10', '0,53', '2,87', '0,27', '1,37', '1,27', '0,17', '1,37', '1,47'], ['0,50', '0,10', '1,67', '0,37', '1,20', '1,10', '0,87', '0,73', '0,33', '0,37', '0,37', '1,90', '0,13', '1,40', '0,97', '0,20', '1,10', '0,90', '0,73', '0,80', '2,53', '0,13', '0,97', '1,13', '0,17', '1,23', '1,33'], ['0,23', '0,40', '2,90', '0,50', '1,40', '1,03', '0,73', '0,57', '0,60', '0,63', '0,53', '1,90', '0,17', '1,37', '0,83', '0,30', '1,03', '0,77', '0,33', '0,40', '2,20', '0,17', '1,33', '1,37', '0,00', '1,03', '1,33'], ['0,10', '0,60', '3,00', '0,67', '1,27', '0,87', '0,43', '0,87', '0,77', '0,43', '0,30', '1,83', '0,20', '1,40', '1,00', '0,10', '0,80', '0,60', '0,23', '0,70', '3,33', '0,47', '1,07', '1,17', '0,20', '1,27', '1,53'], ['0,63', '0,90', '2,67', '0,70', '1,30', '1,00', '0,10', '0,97', '1,27', '0,27', '0,80', '2,93', '0,27', '1,13', '0,67', '0,30', '1,53', '1,00', '0,10', '0,57', '3,13', '0,20', '1,27', '1,23', '0,10', '1,10', '1,57'], ['0,10', '0,97', '3,70', '0,70', '1,30', '0,93', '0,40', '1,20', '1,07', '0,50', '0,70', '2,10', '0,30', '1,37', '0,83', '0,43', '1,20', '0,63', '0,40', '0,13', '2,60', '0,07', '1,60', '1,57', '0,23', '0,73', '1,03'], ['0,57', '0,33', '2,20', '0,67', '1,23', '0,87', '0,57', '0,80', '0,73', '1,00', '0,83', '2,23', '0,13', '1,23', '0,87', '0,33', '0,90', '0,77', '0,67', '0,77', '2,67', '0,17', '1,87', '2,40', '0,07', '1,03', '1,25'], ['0,57', '0,33', '2,37', '0,73', '1,03', '0,57', '0,93', '0,57', '0,47', '0,17', '0,97', '3,23', '0,37', '1,40', '0,87', '0,10', '1,00', '0,70', '0,47', '0,30', '2,93', '0,13', '1,53', '1,83', '0,20', '1,27', '1,97'], ['0,47', '0,93', '2,90', '0,73', '0,90', '0,63', '0,73', '0,70', '0,67', '0,90', '1,23', '2,77', '0,20', '1,30', '0,73', '0,20', '1,13', '0,87', '0,10', '0,57', '2,37', '0,03', '1,77', '2,40', '0,13', '0,93', '1,23'], ['0,13', '0,37', '2,13', '0,70', '1,40', '0,97', '0,43', '0,53', '0,63', '0,13', '0,43', '2,63', '0,03', '1,47', '1,10', '0,17', '1,03', '0,67', '0,17', '0,63', '3,20', '0,13', '1,60', '2,03', '0,10', '1,27', '1,40']]

</div>

</div>

<div class="cell code" execution_count="22">

``` python
# Make the requests for each color pair
for j in range(0, 27, 3):
    for i in range(10):
        L1, C1, H1 = group1[i][j], group1[i][j+1], group1[i][j+2]
        L2, C2, H2 = group2[i][j], group2[i][j+1], group2[i][j+2]
        
        # You can change seperator from comma to dot if you want to use dot seperator with replace function below
        url = url_template.format(L1.replace(',','.'), C1.replace(',','.'), H1.replace(',','.'), L2.replace(',','.'), C2.replace(',','.'), H2.replace(',','.'))
        response = requests.get(url, headers=headers, verify=False)
        
        if response.status_code == 200:
            print(f"Pair {i+1}-{(j//3)+1}: {response.text.replace('.',',')}")
        else:
            print(f"Pair {i+1}-{(j//3)+1} failed with status code: {response.status_code}")
```

<div class="output stream stdout">

    Pair 1-1: 0,1827
    Pair 2-1: 0,7561
    Pair 3-1: 0,3395
    Pair 4-1: 0,1579
    Pair 5-1: 0,1779
    Pair 6-1: 0,5319
    Pair 7-1: 0,3222
    Pair 8-1: 0,2961
    Pair 9-1: 0,401
    Pair 10-1: 0,5039
    Pair 1-2: 0,2214
    Pair 2-2: 0,2787
    Pair 3-2: 0,2609
    Pair 4-2: 0,2838
    Pair 5-2: 0,3156
    Pair 6-2: 0,3688
    Pair 7-2: 0,2664
    Pair 8-2: 0,5085
    Pair 9-2: 0,6152
    Pair 10-2: 0,1942
    Pair 1-3: 0,7362
    Pair 2-3: 0,4679
    Pair 3-3: 0,8033
    Pair 4-3: 0,234
    Pair 5-3: 0,0485
    Pair 6-3: 0,237
    Pair 7-3: 0,5429
    Pair 8-3: 0,4624
    Pair 9-3: 0,323
    Pair 10-3: 0,68
    Pair 1-4: 1,3312
    Pair 2-4: 0,9665
    Pair 3-4: 0,608
    Pair 4-4: 1,3961
    Pair 5-4: 0,0586
    Pair 6-4: 0,5882
    Pair 7-4: 0,4442
    Pair 8-4: 0,1521
    Pair 9-4: 0,9715
    Pair 10-4: 0,5182
    Pair 1-5: 0,1947
    Pair 2-5: 0,1378
    Pair 3-5: 0,2186
    Pair 4-5: 0,1175
    Pair 5-5: 0,3338
    Pair 6-5: 0,6719
    Pair 7-5: 0,1396
    Pair 8-5: 0,3105
    Pair 9-5: 0,1875
    Pair 10-5: 0,6636
    Pair 1-6: 0,1112
    Pair 2-6: 0,5309
    Pair 3-6: 0,0959
    Pair 4-6: 0,2893
    Pair 5-6: 0,5829
    Pair 6-6: 0,2187
    Pair 7-6: 0,3417
    Pair 8-6: 0,1321
    Pair 9-6: 0,1332
    Pair 10-6: 0,5788
    Pair 1-7: 0,2047
    Pair 2-7: 0,3413
    Pair 3-7: 0,1417
    Pair 4-7: 0,587
    Pair 5-7: 0,3539
    Pair 6-7: 0,799
    Pair 7-7: 0,1227
    Pair 8-7: 0,2006
    Pair 9-7: 0,3369
    Pair 10-7: 0,0233
    Pair 1-8: 0,1873
    Pair 2-8: 0,2616
    Pair 3-8: 0,2222
    Pair 4-8: 0,2058
    Pair 5-8: 0,2688
    Pair 6-8: 0,0874
    Pair 7-8: 0,293
    Pair 8-8: 0,2818
    Pair 9-8: 0,1039
    Pair 10-8: 0,0412
    Pair 1-9: 0,1406
    Pair 2-9: 0,0897
    Pair 3-9: 0,3326
    Pair 4-9: 0,2416
    Pair 5-9: 0,2271
    Pair 6-9: 0,5954
    Pair 7-9: 0,2468
    Pair 8-9: 0,0934
    Pair 9-9: 0,2137
    Pair 10-9: 0,2973

</div>

</div>
