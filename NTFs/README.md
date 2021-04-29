# NTFs
Each CloudCoin can hold one NTF. Data can only be uploaded once. Data can be deleted. Once deleted, it can be written to again. 

WARNING: If an NTFs is not authenticated at least once per five years, it will be considered lost and will be recovered by the RAIDA and sold if it has any value. 

## NTFs
SQL
```

mysql> describe nft;
+--------------+---------------+------+-----+-------------------+-----------------------------+
| Field        | Type          | Null | Key | Default           | Extra                       |
+--------------+---------------+------+-----+-------------------+-----------------------------+
| sn           | int(11)       | NO   | PRI | NULL              |                             |
| protocol     | int(11)       | YES  |     | NULL              |                             |
| stripe       | text          | YES  |     | NULL              |                             |
| mirror       | text          | YES  |     | NULL              |                             |
| mirror2      | text          | YES  |     | NULL              |                             |
| created      | timestamp     | NO   |     | CURRENT_TIMESTAMP | on update CURRENT_TIMESTAMP |
+--------------+---------------+------+-----+-------------------+-----------------------------+
5 rows in set (0.00 sec)

```

## Rules
The larger the CloudCoin, the More Data can be stored. 

Note Size | Max Amount of Stripe Data that can be stored | Stripe Data Per RAIDA
------|-----------------|----
250 | 5 MB | 200 KB
100 | 2 MB| 200 KB
 25 | 500 KB| 100 KB
 5 | 250 KB| 25 KB
1 | 50 KB| 2 KB

## Storage Protocol
The user may store their data any way that they like and there may be standards that develop over time. The user can specify there standard with a number.
The standard handles compression, RAID, encryption, file formatting and how to extract meta data. 

Protocol Number | Description
---|---
0 | There is no compression or encryption. The data is stiped, mirrored and then mirrored again. The stipe will be on RAIDA n, the mirror on RAIDA n-3 and the second mirror on RAIDA n-6.

## Services

There are three services

1. detect_ntf
2. insert_ntf
3. delete_ntf

## Detect_data


Sample Call:
```
https://raida0.cloudcoin.global/service/nft/read?sn=8867&an=9dfa64eb6c774635b5ac3e643e8100f1

```
Note that nn, denomination are not needed and are being phased out. PAN is not needed because this service does not change the AN. This service only allows for one coin 
to be detected at once. 

Sample Reqsponse:
```
{
			"server":"raida9",
			"status":"pass",
			"message": "The attached data belongs to the item",
   "storage_protocol": 0,
			"stripe":"b3ZpcG9pd2VyO2xtZ",
			"mirror":"Um5wro7urS7LbunvC",
   "mirror2":"mpsO2VqcmxrZWpyIH",
			"time":"2019-11-08 05:56:32",
   "ex_time":"8.577"
		}

```


## Insert NTF
Each RAIDA will write 

```
https://raida0.cloudcoin.global/service/ntf/insert?
sn=8867&
an=9dfa64eb6c774635b5ac3e643e8100f1
stripe=
mirror=
mirror2=
```

Sample Response
```
Success
```


## Delete NFT
Deletes all the data in an NFT but not the record 
So the coin can never be used again for an NFT unless 
?

Sample Request 
```
HTTPS://Raida0.Cloudcoin.global/service/NFT/delete?sn=677&an=afbb46743568964cf
```
Sample Response 
```
Success
```



