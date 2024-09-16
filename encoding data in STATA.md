### Code Idea

##### Optional step: general cleaning:

```STATA
ds, has(type string) // select variables those have string type to modifid them in next loop
foreach v in `r(varlist)' { // start a loop 
    replace `v' = proper(`v') // convert values to Sentence case
    replace `v' = trim(`v') // trim additional spaces
} // colse the loop

codebook Fruit
```

Result: Before:

![](C:\Users\abdul\AppData\Roaming\marktext\images\2024-09-16-10-27-25-image.png)(screenshot1)

After:

![](C:\Users\abdul\AppData\Roaming\marktext\images\2024-09-16-10-28-23-image.png)(screenshot2)

#### Encoding

This code will encode data alphabatecally and store it in codebook, you can deal with data numirically and display it in string format.

This is my test data:

```STATA
clear // clear workspace
input str10 Fruit Price str10 Date str3 Availability Month
"Banana" 2 "2023-01-31" "Yes" 1
"Apple" 7 "2023-02-28" "No" 2
"Grape" 4 "2023-03-31" "No" 3
"Apple" 9 "2023-04-30" "No" 4
"Banana" 2 "2023-05-31" "Yes" 5
"Banana" 7 "2023-06-30" "No" 6
"Orange" 4 "2023-07-31" "No" 7
"Grape" 4 "2023-08-31" "No" 8
"Orange" 7 "2023-09-30" "Yes" 9
"Mango" 7 "2023-10-31" "No" 10
"Banana" 5 "2023-11-30" "Yes" 11
"Orange" 7 "2023-12-31" "Yes" 12
"Grape" 2 "2024-01-31" "No" 1
"Grape" 8 "2024-02-29" "No" 2
"Orange" 5 "2024-03-31" "No" 3
"Apple" 6 "2024-04-30" "No" 4
"Banana" 9 "2024-05-31" "No" 5
"Apple" 3 "2024-06-30" "Yes" 6
"Mango" 1 "2024-07-31" "No" 7
"Banana" 3 "2024-08-31" "Yes" 8
end
```

| Fruit  | Price | Date       | Availability | Month |
| ------ | ----- | ---------- | ------------ | ----- |
| Banana | 2     | 2023-01-31 | Yes          | 1     |
| Apple  | 7     | 2023-02-28 | No           | 2     |
| Grape  | 4     | 2023-03-31 | No           | 3     |
| Apple  | 9     | 2023-04-30 | No           | 4     |
| Banana | 2     | 2023-05-31 | Yes          | 5     |
| Banana | 7     | 2023-06-30 | No           | 6     |
| Orange | 4     | 2023-07-31 | No           | 7     |
| Grape  | 4     | 2023-08-31 | No           | 8     |
| Orange | 7     | 2023-09-30 | Yes          | 9     |
| Mango  | 7     | 2023-10-31 | No           | 10    |
| Banana | 5     | 2023-11-30 | Yes          | 11    |
| Orange | 7     | 2023-12-31 | Yes          | 12    |
| Grape  | 2     | 2024-01-31 | No           | 1     |
| Grape  | 8     | 2024-02-29 | No           | 2     |
| Orange | 5     | 2024-03-31 | No           | 3     |
| Apple  | 6     | 2024-04-30 | No           | 4     |
| Banana | 9     | 2024-05-31 | No           | 5     |
| Apple  | 3     | 2024-06-30 | Yes          | 6     |
| Mango  | 1     | 2024-07-31 | No           | 7     |
| Banana | 3     | 2024-08-31 | Yes          | 8     |

Check codebook of `Fruit` variable before encoding:

```STATA
codebook Fruit // check before
```

![](C:\Users\abdul\AppData\Roaming\marktext\images\2024-09-16-10-28-23-image.png)(screenshot2)

Encoding all variables using loop:

```STATA
ds, has(type string) // List all string variables
local string_vars `r(varlist)' // Sore them in string_vars list
foreach v of local string_vars { // loop starts
    encode `v', generate(`v'_encoded)
    drop `v'
    rename `v'_encoded `v'
}

codebook Fruit // check after
```

![](C:\Users\abdul\AppData\Roaming\marktext\images\2024-09-16-10-33-42-image.png)(screenshot3)



### Done

Bye

### References

https://nariyoo.com/stata-data-cleaning-with-string-variables-text-data-destring-tostring-encode-and-decode/
