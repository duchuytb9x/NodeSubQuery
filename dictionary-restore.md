# Restoring Data Indexer Projects

Data Indexer Projects indexed on SubQuery Nerwork are usually easy to index, using Postgres Database for storage.

In order to speed up the onboarding of Data Indexer Project, we are providing database snapshots for most of these Project.

## Downloading Database Snapshots

| Project Name | Schema Name | DeploymentId | Database Size | OneDrive URL                                                                                                                   |
| ----------- | ----------- | ------------ | ------------------ | ------------------------------------------------------------------------------------------------------------------------ |
| MerlinMeta | schema_qme58h3kvczyxhe | `Qme58h3kvCZYXHEMuJLo2mHTJSYfGCfQ9Mo4MvKDGPuVyA` | 0.782 GB | `https://phanduchuy-my.sharepoint.com/:u:/g/personal/duchuytb9x_phanduchuy_onmicrosoft_com/EdC4rq4H09VNt1Hmb1vxM3YBl7UMeiLa19mgMIJ2rcFj8w?e=CmH7eB&download=1` |
| Nodle-uniques-mainnet | schema_qmttxz7yyxtsdhb | `QmTTXz7yyxTSDHbSt8fLDbhzwQ3UwWC3jwvwnjZXvDQKuW` | 1.752 GB | `https://phanduchuy-my.sharepoint.com/:u:/g/personal/duchuytb9x_phanduchuy_onmicrosoft_com/EYw8M5fuc3lNun_JNY0xwh0BeFU-K7KuLWTu2AjOmpeOGQ?e=gP1i7d&download=1` |
| Nova Wallet - Altair | schema_qmpktxq1hw1mnt8 | `QmPkTXq1hw1MNt8rVEySAL3izgYa5jRdQbEK9AmERhcM2S` | 1.855 GB | `https://phanduchuy-my.sharepoint.com/:u:/g/personal/duchuytb9x_phanduchuy_onmicrosoft_com/EXCGuA7DW_1JlRG5U9iJ4mIBIU5_b-aUdj8vfdt9kPMKfg?e=kLSBnl&download=1` |
| Nova Wallet - Subsocial | schema_qmwtjalhgb9qekf | `QmWtjALhGB9QEkf2GqVJued71xpLpP4jVUVh4vQDdrgXhv` | 2.477 GB | `https://phanduchuy-my.sharepoint.com/:u:/g/personal/duchuytb9x_phanduchuy_onmicrosoft_com/Ee-ZO-9XPu5Pg5_e5hJwg3QB-TfGSr92XsjyK-VrMRad-w?e=qrGXMa&download=1` |
| Nova Wallet - Kilt | schema_qmpwgk3pbamsra1 | `QmPwGk3PBAmSra1vWriD5Hb3ZKZcGmP2xhCubVgw8JZ5y8` | 2.633 GB | `https://phanduchuy-my.sharepoint.com/:u:/g/personal/duchuytb9x_phanduchuy_onmicrosoft_com/EVmOxY_BtrJBs08Drttb0gYBsh6NKFGKfXMbvYWxAQkNAQ?e=F6FbBj&download=1` |
| Nova Wallet - Basilisk | schema_qmdbxbvjarygtcg | `QmdbxBVjARyGtCgqvyeXN9JAmsskFnVD7ngzrzrBRRknTS` | 3.579 GB | `https://phanduchuy-my.sharepoint.com/:u:/g/personal/duchuytb9x_phanduchuy_onmicrosoft_com/EZ7cgODLSoFCppsLojtp2TgB2Fh6JL1Zo6veXy_fjiHmsw?e=PZqmLq&download=1` |
| Nova Wallet - Quartz | schema_qmaujqgjmw8ufsf | `QmaUJQgjMw8ufsFW8nPnbgP3iGRknhKHB3z6S1WyHahsZ8` | 3.698 GB | `https://phanduchuy-my.sharepoint.com/:u:/g/personal/duchuytb9x_phanduchuy_onmicrosoft_com/EYQHsftYkRpLtm93q81GwSkBPc8QAKKMU_6oZqXhfIGefA?e=Vq6pSw&download=1` |
| WeFi-XDC | schema_qmqdbjk5vf2jjns | `QmQDBjk5vf2jjnS2gk5tweE2pUWRhRzGpwU181TXwmQknv` | 4.031 GB | `https://phanduchuy-my.sharepoint.com/:u:/g/personal/duchuytb9x_phanduchuy_onmicrosoft_com/EcUs7j79ZPpInHP0Zmmm_SQBrtZNCduHrmVtk37DAST3cw?e=zBvGCW&download=1` |
| Nodle stats | schema_qmeyyergejvu26s | `QmeYyergeJvU26s9g46yXBEA8216vBmzpYZYjLQeW9MSb1` | 4.927 GB | `https://phanduchuy-my.sharepoint.com/:u:/g/personal/duchuytb9x_phanduchuy_onmicrosoft_com/EWBjlPz9MXhPoQ3IuEKvmlkBZh2ceWlrJpaYxF3GQmYY9g?e=jIl5QF&download=1` |
| [ARCHIVED] SubQuery Seekers Quest - Metis | schema_qmwfocenf5yapnd | `QmWfoceNf5YApNdS6srEMBwUY3NKxWBDE2HuKoSokRpBws` | 5.106 GB | `https://phanduchuy-my.sharepoint.com/:u:/g/personal/duchuytb9x_phanduchuy_onmicrosoft_com/ETwqrpW_xxhKiwKF6e83X8EBjQ3qoCe_aQHwRI5NlELf3A?e=m4cU5I&download=1` |
| SQ Network Main | schema_qmschygv2fyjub2 | `QmScHyGv2fyJUB2prBKCKx3i8kGrQ3wU7USq8yBJ9DWiG9` | 5.167 GB | `https://phanduchuy-my.sharepoint.com/:u:/g/personal/duchuytb9x_phanduchuy_onmicrosoft_com/ER0Y6CZiZ0xNqyFNa6xZrLABMT1MlfR_KXGB_JiiZ0d71Q?e=yBbfZD&download=1` |
| Nova Wallet - Bit Country | schema_qmd3hcvgc61hwxf | `Qmd3hcVGc61HWxFF9JYVYn2LuxMXZxZqGq58XLxEq6TGpy` | 7.184 GB | `https://phanduchuy-my.sharepoint.com/:u:/g/personal/duchuytb9x_phanduchuy_onmicrosoft_com/EWqXDjMfqMlNnwffCOWIu6QB-3ypg_zoKrDo_HI3PwHeig?e=qrctBZ&download=1` |
| Noval Wallet - Polkadex | schema_qmdzl852vgngmdm | `QmdzL852vGNgmdmk4UdvpPWeVsTtYJiMsjJd6ZxnSbQsfP` | 7.74 GB | `https://phanduchuy-my.sharepoint.com/:u:/g/personal/duchuytb9x_phanduchuy_onmicrosoft_com/EdINJQij2cVLt4veMjqQ4U0B5hBTQHG61DAf14S8vdj0pw?e=i6FRs1&download=1` |
| Nova Wallet - Statemint | schema_qmweqzwnrmhuvac | `QmWeQZWNrmHUvac2yz9ePpQqVwJM9QFpK9ULwt7ype3CmP` | 9.245 | `https://phanduchuy-my.sharepoint.com/:u:/g/personal/duchuytb9x_phanduchuy_onmicrosoft_com/EXB-6ymO9hROkcnxo7OkGwUBfDB6Ij8OfEeecMch2kW_kQ?e=yIfKq3&download=1` |
| Asset Hub (former Statemint) Dictionary | schema_qme1iqvwloeh1zl | `Qme1iQvwLoeh1ZLZVL4zDGZBK1hnMG3xZz1oaLBRvZxT7X` | 10 GB | `https://phanduchuy-my.sharepoint.com/:u:/g/personal/duchuytb9x_phanduchuy_onmicrosoft_com/EbMnvT1UmOFLtv7KwFQ3VZgBD3mGk0ZPioru_dzmDdK5kA?e=qjfybo&download=1` |
| Nova Wallet - Karura | schema_qmuao3knuikplwz | `QmUAo3KNUiKpLwZXoygCF5cFLFxBoNbwWYJmhwQba672Dn` | 13 GB | `https://phanduchuy-my.sharepoint.com/:u:/g/personal/duchuytb9x_phanduchuy_onmicrosoft_com/EQTwa0M7DqBLhduiXltcSWYBG8Yl8wzM0vM-_wYdVUAzIg?e=XzFARG&download=1` |
| Bifrost (Kusama) Dictionary | schema_qmcvcn4gzkib2jk | `QmcvcN4gZkiB2JkmK6BdHh7Wzy8Gfp8R7ZHSgGajbGv6Wy` | 14 GB | `https://phanduchuy-my.sharepoint.com/:u:/g/personal/duchuytb9x_phanduchuy_onmicrosoft_com/EWlPftQ8JFZFg0eUkNCrisQBtPS2Sk1bXxDlPnbfzxg3lA?e=VIlrMw&download=1` |
| Nova Wallet - Picasso | schema_qmpyabw93fkwx8z | `QmPYABw93FKwx8zhzzCw6J69Y664RzFn8mUmThUsP1YWUR` | 14 GB | `https://phanduchuy-my.sharepoint.com/:u:/g/personal/duchuytb9x_phanduchuy_onmicrosoft_com/EYSoeMIRtm1LmUs7Svkmzr8B6VT9kxa1phdwJVu64OAs7g?e=ZVyrM4&download=1` |
| Nova Wallet - Acala | schema_qmekuwv1thjerbo | `QmeKUwv1ThJerboGV8t6zBYGCpJXkht1QMHY6QMU9xmWWm` | 15 GB | `https://phanduchuy-my.sharepoint.com/:u:/g/personal/duchuytb9x_phanduchuy_onmicrosoft_com/EVIzfDKksQZLpXWLxAY8sokByGZmJFgL_anLqGsqyLxB4A?e=W1iMLa&download=1` |
| Acala Dictionary | schema_qmuj8yyce1yu5un | `QmUj8yYCE1YU5UNdtm4q4di4GBDEAmL8vprSRWVGrYeEFm` | 16 GB | `https://phanduchuy-my.sharepoint.com/:u:/g/personal/duchuytb9x_phanduchuy_onmicrosoft_com/EWsC0EIzMedNmVlXTcLFJE4BLiWuyOHzicNnWlUWwjfhbA?e=S4uMNv&download=1` |
| Karura Dictionary | schema_qmpqqa28fxr1hep | `QmPQQA28fxR1hePk25MHNS1vEYRs4Gbz3PXry8G4dfC76N` | 17 GB  | `https://phanduchuy-my.sharepoint.com/:u:/g/personal/duchuytb9x_phanduchuy_onmicrosoft_com/ESUjyz-p_qBErx4o_rm_EUEBWgPn1ZTfVLEbaRMsxFAT0w?e=Zgm5jA&download=1` |
| Calamari Dictionary | schema_qmdrqzazvsmrr6r | `QmdrqzazvSmrr6rgfxJEssJH9jqhYCZARm92UxNXMv5f86` | 18 GB  | `https://phanduchuy-my.sharepoint.com/:u:/g/personal/duchuytb9x_phanduchuy_onmicrosoft_com/EXbWtQIKWcVLiDxxZaiec50BaINAIcMlMpN0zkjTNV6S6A?e=NNQYtF&download=1` |
| Nova Wallet - Calamari | schema_qmebhtyhbcqjtjg | `QmeBhTYHBcqJTJgfN7HDeSM4nHFR1c7fryZfRxGmRpwNHU` | 19 GB | `https://phanduchuy-my.sharepoint.com/:u:/g/personal/duchuytb9x_phanduchuy_onmicrosoft_com/ET3itcpUO35Fu3Hbk4RxCZ4Bmo_6LMXIaUwP8zg6AukcQg?e=RFjr89&download=1` |
| Nova Wallet - Shiden | schema_qmvkg3gjejcpwkx | `QmVKG3gJejcPwKXHP1Yhk1tVTzKh4EZshpJSQyFtCeZkhc` | 21 GB | `https://phanduchuy-my.sharepoint.com/:u:/g/personal/duchuytb9x_phanduchuy_onmicrosoft_com/Ec8BbBbvQbdFsQMDO0_A2bMBlDC9h-xWhOvdhuaf8TnCLA?e=UbozbT&download=1` |
| Moonbase Alpha Dictionary | schema_qmwv9ja5aq9cppx | `QmWv9Ja5AQ9cPpXb6U7sGCvkhK6XbZ7xQntTBqidsSf5SF` | 26 GB | `https://phanduchuy-my.sharepoint.com/:u:/g/personal/duchuytb9x_phanduchuy_onmicrosoft_com/ERmtT_9RoS5LsRryzBu8MykBgNWXxG-N2r6BMAOi_USlTA?e=eIKJf3&download=1` |
| Shiden Dictionary | schema_qmpitswpmteipwn | `QmPiTswpMTeipwnmJkAcwkcg5Se8XfrucGYVKbwuAxQgJ6` | 27 GB | `https://phanduchuy-my.sharepoint.com/:u:/g/personal/duchuytb9x_phanduchuy_onmicrosoft_com/EXLpaqS2R4tAsbUNROcWGOYBtEW8XuBm-gii-xYl-SUIKQ?e=5eeURE&download=1` |
| Nova Wallet - Bifrost | schema_qmr5tfcmaod162b | `QmR5tfCMAoD162BpR1DxqvtZue5rQPQrMGqSHc4SsWS2ap` | 33 GB | `https://phanduchuy-my.sharepoint.com/:u:/g/personal/duchuytb9x_phanduchuy_onmicrosoft_com/EV3VE3dYnJJCtB8JyIy0LGQB-a5tPiD7k5UbzS2nkOqZkg?e=5mlIIh&download=1` |
| Kilt Spiritnet Dictionary | schema_qmebtnuhahuo2eh | `QmeBTNuhahUo2EhTRxV3qVAVf5bC8zVQRrrHd3SUDXgtbF` | 39 GB | `https://phanduchuy-my.sharepoint.com/:u:/g/personal/duchuytb9x_phanduchuy_onmicrosoft_com/ETNmGtHNu0NHumPeZB--RAMBJ-_7aPZwY6bRh508Jpz0gw?e=S2sPaf&download=1` |
| Nodle Parachain Dictionary | schema_qmzpj5wypubgqjd | `QmZpj5wYpUbGqJDg6KWgbkK5bmeuCqYX6kwk317jdJ9DZ4` | 47 GB | `https://phanduchuy-my.sharepoint.com/:u:/g/personal/duchuytb9x_phanduchuy_onmicrosoft_com/EXRJOJJFk0BFou5neaUEqzsB5A6VEyjwF4hGACm4-vEy_g?e=bpu5a4&download=1` |
| Nova Wallet - Aleph Zero | schema_qmemyqvhn7yxcht | `QmeMyqVHN7YxCHT6ftpaJ26APMCAPi4VfV5T1Zj8o8Cy3c` | 50 GB | `https://phanduchuy-my.sharepoint.com/:u:/g/personal/duchuytb9x_phanduchuy_onmicrosoft_com/EdXVxaXLoshJpH25loyQaSQBN2QiAeV2Gyi8UxZ6upPpxQ?e=hCJwoS&download=1` |
| Westend Dictionary | schema_qmp1bmjoyj5ifq6 | `QmP1BMJoyJ5iFq6XLSfTJ3D23iWuTG1tnsEffJpNieQnwN` | 54 GB | `https://phanduchuy-my.sharepoint.com/:u:/g/personal/duchuytb9x_phanduchuy_onmicrosoft_com/Een-GU878BBJvm3LjvwuVIgBq44oQ9rue_VyHwej7Zyn3g?e=VUqklI&download=1` |
| Nova Wallet - Moonbeam | schema_qmwmm1teaazm699 | `QmWmm1teaAzm699PBQQ6MuEEmbNJubXHyTpWqCWKurqSNs` | 60 GB | `https://phanduchuy-my.sharepoint.com/:u:/g/personal/duchuytb9x_phanduchuy_onmicrosoft_com/EU1kgTcrQh5HgDcMIuYBbL0BfVAfOXPn6mPnU9S5dxDLIw?e=h4K8uV&download=1` |
| Aleph Zero Dictionary | schema_qmayr3cjyhywww1 | `QmaYR3CJyhywww1Cf5TMJP15DAcD3YE9ZSNmdLbM7KiQHi` | 77 GB | `https://phanduchuy-my.sharepoint.com/:u:/g/personal/duchuytb9x_phanduchuy_onmicrosoft_com/ERxi68pRKstHiEvGWstC5dABg9cwF-WzvqHqgYdIcIgj4w?e=WCTHIi&download=1` |
| Nova Wallet - Moonriver | schema_qmdbhaq6mfjnhvk | `QmdbhaQ6mFJNHVk5WbNyFsevfJysiXyueMRHqWN7FTXMtN` | 81 GB | `https://phanduchuy-my.sharepoint.com/:u:/g/personal/duchuytb9x_phanduchuy_onmicrosoft_com/EfHwMG_rQ8FLs39zrvDUzj4BUP2sUD1xJKvbqjqY29EMxw?e=8CHIdX&download=1` |
| B2 Meta | schema_qmq3hsukp2pk6nd | `QmQ3hSUkP2Pk6nDKJZ7ErDqKTu1hrdZmkrxXHApZGsb4ZF` | 96 GB | `https://phanduchuy-my.sharepoint.com/:u:/g/personal/duchuytb9x_phanduchuy_onmicrosoft_com/EbNajUMQxqFFhjm1eLWzbU4B4g2FqF-1lZPj06ts8cctRg?e=vtl7ZJ&download=1` |
| Nova Wallet - Astar | schema_qmwd7swh7auyvvy | `QmWD7SwH7aUyVvyydZRzS7XtM8bSU6izkvWgzYgrtw3V82` | 98 GB | `https://phanduchuy-my.sharepoint.com/:u:/g/personal/duchuytb9x_phanduchuy_onmicrosoft_com/ESGTj8aks0lJodvB3YcfZaMBg8UAZCpzUNEsTp5q4_m2Aw?e=EhBCEf&download=1` |
| Nova Wallet - Kusama | schema_qmbqmlgzmofehas | `QmbQmLgzmoFEhAsMZDB4pGZYznXHZSHENMki1ymbDowehY` | 128 GB | `https://phanduchuy-my.sharepoint.com/:u:/g/personal/duchuytb9x_phanduchuy_onmicrosoft_com/EeV6eEgSciVFl34oZ9pvXo0BKmWUUDKZykIaqy0uK5abqA?e=aHUmSj&download=1` |
| Nova Wallet - Polkadot | schema_qmfvylpfjkvt7dk | `QmfVyLpFjkvT7DKU8hdqBpxKR677ak6bo7jeU68XsCPHLZ` | 141 GB | `https://phanduchuy-my.sharepoint.com/:u:/g/personal/duchuytb9x_phanduchuy_onmicrosoft_com/ET4z1iBeTJZLjYTe1vaifeABYaxe7XUr4W02D7VVWbvwPA?e=uZksQd&download=1` |
| Kusama Dictionary | schema_qmbe5g5vbejyyaf | `Qmbe5g5vbEJYYAfpjcwNDzuhjeyaEQPQbxKyKx6PveYnR8` | 179 GB | `https://phanduchuy-my.sharepoint.com/:u:/g/personal/duchuytb9x_phanduchuy_onmicrosoft_com/EUW09ALVgN9CkCauYWGpE2EB9Ya3rsME5lFELWDmtx8LFA?e=DJY2VO&download=1` |
| Mode Meta | schema_qmstc9wof5jwfgw | `QmStc9Wof5JwfGwjs2WjoWjEYzGKQ6Jo8UsLJMr9QYBAv6` | 188 GB | `https://phanduchuy-my.sharepoint.com/:u:/g/personal/duchuytb9x_phanduchuy_onmicrosoft_com/EaqDaYnvqFFKl9FXIug-OC0BpPuCnv089bNKRHvZK_20Qw?e=2KbC9U&download=1` |
| Astar Dictionary | schema_qmapq6cnkptze1j | `QmapQ6cNKPtZE1jkeUp5V6xy7sPSiJiZpoqZcRRtyc4Stq` | 189 GB | `https://phanduchuy-my.sharepoint.com/:u:/g/personal/duchuytb9x_phanduchuy_onmicrosoft_com/EbcZMFnnB1xNh9bYF0KGGCIBMhz6GrTHbek6dzsgBUsrIg?e=aTw4uy&download=1` |
| Moonriver Dictionary | schema_qmwhwlqa4p6izv6 | `QmWhwLQA4P6iZv6bmQxUqG5zumNK8KDBwcq8wxN4G213dq` | 216 GB | `https://phanduchuy-my.sharepoint.com/:u:/g/personal/duchuytb9x_phanduchuy_onmicrosoft_com/EVKjxZfxmJVHuEwl7HFeXHgB-rCsJUBbYsW2QRscz5sSmQ?e=SrgVxo&download=1` |
| Nova Wallet - Khala | schema_qmbtvvmnw2xsfrl | `QmbtvVmnw2xsFrLEyp5oQWfunmaoDcJYPDttDHofkSM5j2` | 258 GB | `https://phanduchuy-my.sharepoint.com/:u:/g/personal/duchuytb9x_phanduchuy_onmicrosoft_com/EcGtzuzoYmRCmaYj6iVo4sIB7ZQj92Nv21rZKkTrE8DQpg?e=UiUZaj&download=1` |
| Moonbeam Dictionary | schema_qmuhasweqyxyry5 | `QmUHAsweQYXYrY5Swbt1eHkUwnE5iLc7w9Fh62JY6guXEK` | 288 GB | `https://phanduchuy-my.sharepoint.com/:u:/g/personal/duchuytb9x_phanduchuy_onmicrosoft_com/EUTdl_cHrHJIrR2UlvO9Y8QBztzsCjfvtX9J496Sx9FejA?e=XfvB3C&download=1` |
| Polkadot Dictionary | schema_qmugbdhqknze8q6 | `QmUGBdhQKnzE8q6x6MPqP6LNZGa8gzXf5gkdmhzWjdFGfL` | 406 GB | `https://phanduchuy-my.sharepoint.com/:u:/g/personal/duchuytb9x_phanduchuy_onmicrosoft_com/ESacL9c7-XVDobbTeYOYo2wBHMaER6vDeN5g4UF4bs2dbw?e=JN0l9T&download=1` |
| Khala Dictionary | schema_qmp2krbgx4vlal8 | `QmP2KRbGx4vLaL8HqugVXrNPMyziFL6aM9NAd4NbFqsPA9` | 424 GB | `https://phanduchuy-my.sharepoint.com/:u:/g/personal/duchuytb9x_phanduchuy_onmicrosoft_com/EdZeALcfYcpKir2OmOjw10wBNPV7mG2TCcQUlPSTxMUZRg?e=sFvTew&download=1` |                                                                                           

You can download the snapshot either from wget link:

### Download Snapshot

```bash
wget "https://phanduchuy-my.sharepoint.com/:u:/g/personal/duchuytb9x_phanduchuy_onmicrosoft_com/EUW09ALVgN9CkCauYWGpE2EB9Ya3rsME5lFELWDmtx8LFA?e=DJY2VO&download=1" -O schema_qmbe5g5vbejyyaf.dump
```

## Restoring the Database Snapshot

1. Copy the `schema_xxxxxxx.dump` to `/root/subquery-indexer/.data/postgres` and then use this command:


```bash
cp /root/polkadot/schema_qmbe5g5vbejyyaf.dump /root/subquery-indexer/.data/postgres/schema_qmbe5g5vbejyyaf.dump
```

2. Run this command in `tmux`:

```bash
docker exec -it indexer_db pg_restore -v -j 5 -h localhost -p 5432 -U postgres -d postgres /var/lib/postgresql/data/schema_qmbe5g5vbejyyaf.dump > /root/restore.log 2>&1
```

>Note
>
>We use the `-j` parameter to update the number of jobs running concurrently. Depending on your machine size, you may want to increase this number to speed up the restore process. [Read more](https://www.postgresql.org/docs/current/app-pgrestore.html)

The restore process will start and take quite a long time (like 2 days), please make sure you run this cmd in the background (use tools like tmux/screen/nohup). Here is an example of the output log.

```
pg_restore: connecting to database for restore
pg_restore: processing item 5081 ENCODING ENCODING
pg_restore: processing item 5082 STDSTRINGS STDSTRINGS
pg_restore: processing item 5083 SEARCHPATH SEARCHPATH
pg_restore: processing item 5084 DATABASE postgres
pg_restore: processing item 5085 COMMENT DATABASE postgres
pg_restore: processing item 50 SCHEMA schema_qmbe5g5vbejyyaf
pg_restore: creating SCHEMA "schema_qmbe5g5vbejyyaf"
pg_restore: processing item 892 FUNCTION schema_notification()
pg_restore: creating FUNCTION "schema_qmbe5g5vbejyyaf.schema_notification()"
pg_restore: processing item 313 TABLE _metadata
pg_restore: creating TABLE "schema_qmbe5g5vbejyyaf._metadata"
pg_restore: processing item 312 TABLE _poi
pg_restore: creating TABLE "schema_qmbe5g5vbejyyaf._poi"
pg_restore: processing item 315 TABLE events
pg_restore: creating TABLE "schema_qmbe5g5vbejyyaf.events"
pg_restore: processing item 316 TABLE extrinsics
pg_restore: creating TABLE "schema_qmbe5g5vbejyyaf.extrinsics"
pg_restore: processing item 314 TABLE spec_versions
pg_restore: creating TABLE "schema_qmbe5g5vbejyyaf.spec_versions"
pg_restore: entering main parallel loop
pg_restore: launching item 5078 TABLE DATA extrinsics
pg_restore: launching item 5074 TABLE DATA _poi
pg_restore: launching item 5077 TABLE DATA events
pg_restore: launching item 5075 TABLE DATA _metadata
pg_restore: launching item 5076 TABLE DATA spec_versions
pg_restore: processing data for table "schema_qmbe5g5vbejyyaf.extrinsics"
pg_restore: processing data for table "schema_qmbe5g5vbejyyaf._metadata"
pg_restore: processing data for table "schema_qmbe5g5vbejyyaf.events"
pg_restore: processing data for table "schema_qmbe5g5vbejyyaf._poi"
pg_restore: processing data for table "schema_qmbe5g5vbejyyaf.spec_versions"
pg_restore: finished item 5075 TABLE DATA _metadata
pg_restore: launching item 4934 CONSTRAINT _metadata _metadata_pkey
pg_restore: creating CONSTRAINT "schema_qmbe5g5vbejyyaf._metadata _metadata_pkey"
pg_restore: finished item 5076 TABLE DATA spec_versions
pg_restore: launching item 4936 CONSTRAINT spec_versions spec_versions_pkey
pg_restore: creating CONSTRAINT "schema_qmbe5g5vbejyyaf.spec_versions spec_versions_pkey"
pg_restore: finished item 4936 CONSTRAINT spec_versions spec_versions_pkey
pg_restore: finished item 4934 CONSTRAINT _metadata _metadata_pkey
pg_restore: launching item 4947 TRIGGER _metadata 0x2617a822749f1a95
pg_restore: creating TRIGGER "schema_qmbe5g5vbejyyaf._metadata 0x2617a822749f1a95"
pg_restore: finished item 4947 TRIGGER _metadata 0x2617a822749f1a95
pg_restore: finished item 5074 TABLE DATA _poi
pg_restore: launching item 4926 CONSTRAINT _poi _poi_chainBlockHash_key
pg_restore: creating CONSTRAINT "schema_qmbe5g5vbejyyaf._poi _poi_chainBlockHash_key"
pg_restore: finished item 4926 CONSTRAINT _poi _poi_chainBlockHash_key
pg_restore: launching item 4928 CONSTRAINT _poi _poi_hash_key
pg_restore: creating CONSTRAINT "schema_qmbe5g5vbejyyaf._poi _poi_hash_key"
pg_restore: finished item 5078 TABLE DATA extrinsics
pg_restore: launching item 4942 INDEX 0x288575ef7a7aaf75
pg_restore: launching item 4943 INDEX 0x57c58da22539b57d
pg_restore: launching item 4944 INDEX 0x5b57ecd94445ad2e
pg_restore: creating INDEX "schema_qmbe5g5vbejyyaf.0x288575ef7a7aaf75"
pg_restore:pg_restore:  creating INDEX "schema_qmbe5g5vbejyyaf.0x5b57ecd94445ad2e"
creating INDEX "schema_qmbe5g5vbejyyaf.0x57c58da22539b57d"
pg_restore: finished item 4928 CONSTRAINT _poi _poi_hash_key
pg_restore: launching item 4932 CONSTRAINT _poi _poi_pkey
pg_restore: creating CONSTRAINT "schema_qmbe5g5vbejyyaf._poi _poi_pkey"
pg_restore: finished item 4932 CONSTRAINT _poi _poi_pkey
pg_restore: launching item 4930 CONSTRAINT _poi _poi_parentHash_key
pg_restore: creating CONSTRAINT "schema_qmbe5g5vbejyyaf._poi _poi_parentHash_key"
pg_restore: finished item 4944 INDEX 0x5b57ecd94445ad2e
pg_restore: finished item 4942 INDEX 0x288575ef7a7aaf75
pg_restore: finished item 4930 CONSTRAINT _poi _poi_parentHash_key
pg_restore: finished item 4943 INDEX 0x57c58da22539b57d
pg_restore: launching item 4946 CONSTRAINT extrinsics extrinsics_pkey
pg_restore: creating CONSTRAINT "schema_qmbe5g5vbejyyaf.extrinsics extrinsics_pkey"
pg_restore: finished item 4946 CONSTRAINT extrinsics extrinsics_pkey
pg_restore: finished item 5077 TABLE DATA events
pg_restore: launching item 4937 INDEX 0x46e7a495bb4c21d1
pg_restore: launching item 4938 INDEX 0x62b8f3181611d490
pg_restore: launching item 4939 INDEX 0xc0c9768d1987b60f
pg_restore: creating INDEX "schema_qmbe5g5vbejyyaf.0x46e7a495bb4c21d1"
pg_restore: pg_restore:creating INDEX "schema_qmbe5g5vbejyyaf.0x62b8f3181611d490"
 creating INDEX "schema_qmbe5g5vbejyyaf.0xc0c9768d1987b60f"
pg_restore: finished item 4939 INDEX 0xc0c9768d1987b60f
pg_restore: finished item 4938 INDEX 0x62b8f3181611d490
pg_restore: finished item 4937 INDEX 0x46e7a495bb4c21d1
pg_restore: launching item 4941 CONSTRAINT events events_pkey
pg_restore: creating CONSTRAINT "schema_qmbe5g5vbejyyaf.events events_pkey"
pg_restore: finished item 4941 CONSTRAINT events events_pkey
pg_restore: finished main parallel loop
```

After the data restored, you can start adding the specific project to you service inside admin app, and start indexing the project, the indexing will start basing on the restored data and continue indexing the project.
