## Setup 
Clone the repo
  ```git clone https://github.com/fai555/Istio-and-JWT.git```


Setup a environment
  ```
  cd 
  virtualenv -p python3 env
  pip install -r requirements.txt
  ```

## Generate Public/Private Key Pair Using OpenSSL

```
chmod +x generate-pem-key-pairs.sh

./generate-pem-key-pairs.sh
```

## Generate JWT Using the Private Key Generated in Previous Step
```
python generate-token-using-pem-files.py
```

## Generate RSA Public/Private Key Pairs and JWT Using Python
```
python generate-keys-and-tokens-using-python.py
```

## Create a JWKS - JSON Web Key Set
You need your public key in JSON format to create JWKS. You will get the public keys in JSON format in the last 2 steps. Whichever you may choose to use.

An example public key is 

```
{"e":"AQAB","kty":"RSA","n":"3LlzeRY6gbIVwGO7AxO1bN3-CgWwIpWOT8m485AzkOdhxgCWc2F-3OqAigDyyDMqXtH1ovCaZnEIf3ZkJin7Y_zC48TNQwlKnuM29CrTjnYR1c_w30ZT4PNIisEwLKuEX5uRHuIrKYBxwwVf4eqoFmtpZbrmwDPCA1ZMFox0v40q1m_SecCB286alE42Ohb6j0ZuntjO5rg2ZyQt3EmxEDPE2Iuh737gYhXLuFhTiYH5S_kFokX1Yv0RdUyiGcmaxXgGaF3iglnsOHv9209uwlzrcDAouOD7PYbLjCoqpWydVLyxcJGqjF5i7CK36q_SVmpGHbIsdOlZQLWNA97AgQ"}
```

Then you need to encapsulate this key as an item in the following array. Like this.

```
{ "keys":[ 


{"e":"AQAB","kty":"RSA","n":"3LlzeRY6gbIVwGO7AxO1bN3-CgWwIpWOT8m485AzkOdhxgCWc2F-3OqAigDyyDMqXtH1ovCaZnEIf3ZkJin7Y_zC48TNQwlKnuM29CrTjnYR1c_w30ZT4PNIisEwLKuEX5uRHuIrKYBxwwVf4eqoFmtpZbrmwDPCA1ZMFox0v40q1m_SecCB286alE42Ohb6j0ZuntjO5rg2ZyQt3EmxEDPE2Iuh737gYhXLuFhTiYH5S_kFokX1Yv0RdUyiGcmaxXgGaF3iglnsOHv9209uwlzrcDAouOD7PYbLjCoqpWydVLyxcJGqjF5i7CK36q_SVmpGHbIsdOlZQLWNA97AgQ"}

]}
```

This is a valid JWKS.

## Create a JWKSURI - JSON Web Key Set URI
Put the JWKS created above in a publicly accessible place. I will be storing it in this public repo as a json file. The JWKS is stored in the ```json-web-key-set.json``` file. You can use the raw file URL from GitHub and use it in Istio.





_________________PUBLIC___________________

{"e":"AQAB","kty":"RSA","n":"t91SsRbsZEDin8Res5ms2-vqzCaJeFhvHRSuNrwVV3eC9luHdfq1cFN60VV9e12Xa0auLG4TLVb1AcC2-2kZXYCSHcrQdgceEprml89IuMhK-xdXU3iMlfYRAK3hJ460jo46__qyEx0q3Jj5ZvcGAJTVgTM4vGQ6fro8QDtJjO1UQ2kCj16c3R7ACqSiNQ0_3CHBImpzos5NKmXEODr4THHeDYonDatV_mUaqerr_H_svyaDZIYFKniDhgBXhsq77Sd9AhqyR4akpbB9IvmosCLP8Ohc6hdrNzUjmMq62bHw_twK8FEOvq2ow-PKFO6wh53GxmtoNj6n0jcFep2rDw"}

_________________PRIVATE___________________

{"d":"N13fY9JqVvovBDtm5SB2rDcLmnRUWzgOJayvlW3n41HqzvLbBMz9TBjnWBgtVDPnv_clxd1TywhveRqmP2jzqXNpDK2hPpmAFcwtejOCS5qM8bWip1EazKGvlwvFTFstxevQmnrMmvLikFFEcRwb45rt_B0HjbuE3dqJADKaQGRIRjFMCAVrOHF4baIuJzvkVrzATgEiU0jnERVvvQzLZt7jNwP3BFf37FYJ_JFIA90upQbetBS8Wpu0UDdsp1Wb2muoXzILscQsTW8sSExmwfu3IoMOf4IYrGDoi64u7UDXxWFJ5QCqa8bCqon6UMorwBjiXia1f5EOKfb61yiQyQ","dp":"zw6adiCaQm2lqMle1VPZbGngJPF6NlH1UOqYyXu6y48EhBF5rMCinnzpd7rZysmKTX5XdJqfQWUgdInrZg6Ba9HBZpPhG8WCi8_RZy4_yJmSj6YsDezZaqgZF4WE0Ra16F5uyGhhliA92C-A8eJpnQfhYuQyGXu41iopVOR4HqU","dq":"Sp3grqOtfvd89w1t7bmVgjeltwA_CcoS0OgFWu1ivPiqtUaiR1ZCOZmXSZiZhS833HAOR7hptM3il0ujcn4jWc7CxaF1TXzLUDAUNyiz2P9wHvyEmcEq52yrnimJ8bLF4-0BFFo9ve4YuhYzSR0tdgk5EwN1un1JzDqf587CEY8","e":"AQAB","kty":"RSA","n":"t91SsRbsZEDin8Res5ms2-vqzCaJeFhvHRSuNrwVV3eC9luHdfq1cFN60VV9e12Xa0auLG4TLVb1AcC2-2kZXYCSHcrQdgceEprml89IuMhK-xdXU3iMlfYRAK3hJ460jo46__qyEx0q3Jj5ZvcGAJTVgTM4vGQ6fro8QDtJjO1UQ2kCj16c3R7ACqSiNQ0_3CHBImpzos5NKmXEODr4THHeDYonDatV_mUaqerr_H_svyaDZIYFKniDhgBXhsq77Sd9AhqyR4akpbB9IvmosCLP8Ohc6hdrNzUjmMq62bHw_twK8FEOvq2ow-PKFO6wh53GxmtoNj6n0jcFep2rDw","p":"6R2d9XMxcKzr8Y2qGvhkBktoM1aTXoOE0lZakYr51edLJB55v-GriDg4oPpvR7q_kozvllJDt6GvKsUroWKrx35XPrI5P7stCOp6Z19-WRQyBF_n4gdS5pC_dfA2oc9z5lqC_NNU4lGLNIvfVtumZ9soOKIJZGw_q7ddIwBMkg0","q":"yen8Q3vqgcqepLr57zAudu1XxXY1BUPgs43zPb-aTBP-1jAW-rXCwTNOfxLsAmr14XOCIKXs1qfT1Dh5U4gyD1lglYzAlAFRtSKkkfaU_puVj_vPUQSrHet2Z-AJa6pK2DEDnmialKL6fq7oxR5EwvFvdyR8U4lc6uq5PKtiVos","qi":"W8R4TnZcXETfD9mPYECO06wcOeNGa4-W94FEsAkJHgrX27bCB_MhyAkWj91cOHOYPscm9ODPn3N_mCG8jfxYjv62zw_2ooKy4ZKymkf3AvcorK92UXGd8vAoN7-_Fpf1pqfKxXzOPAFci1LyzgUd2ota2xi5XbDCYZNZU_UIZiE"}

_________________TOKEN___________________

eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJBVURJRU5DRSIsImV4cCI6MTY0OTUwNzQ4NiwiaWF0IjoxNjQ5NTA0NDg2LCJpc3MiOiJJU1NVRVIiLCJqdGkiOiJPME9pUU1QOTV6LXBQaGRfZm1HaWZnIiwibmJmIjoxNjQ5NTA0NDg2LCJwZXJtaXNzaW9uIjoicmVhZCIsInJvbGUiOiJ1c2VyIiwic3ViIjoiU1VCSkVDVCJ9.XBnIZhqGGelhGv-5b1spwUtAbCP5wGFxdBoqlr0of27lGLtCn0-_a9Ckr1rKPzWYvVsIdph730cxrQu6JnOFLAIX8yLvjdCaBDitDjmt-ZfAaDz1qtCtF5YRbUvMWTOfcFrOZLbZBOVGhfDC3BQ3j84ibqk9Bvlgqhn2_NXDwVkiEGpJk-YRa3Ry7IC0Jfto55zl1_57Y5FP8g4GCSF4GtRuEvLfatbF5c8kjMTGGEsmYYgiheKDCNwpNvcRSIHoLNjuMW64aIfhW4hQZ8VGkmeivtjTAWTomzP8QfJtFFyciQ0bpxabHewCmA0kiWTi1c3NRh3pycDHQcbOPud9xA

_________________TOKEN INFO___________________

{'alg': 'RS256', 'typ': 'JWT'}
{'aud': 'AUDIENCE', 'exp': 1649507486, 'iat': 1649504486, 'iss': 'ISSUER', 'jti': 'O0OiQMP95z-pPhd_fmGifg', 'nbf': 1649504486, 'permission': 'read', 'role': 'user', 'sub': 'SUBJECT'}




Jwt Issuer is not configured
 => JWKS kısmında sorun var ise 
 
Jwt verification Failed
 => JWT - JWKS ile uyumsuz (örn: issuer farklı olabilir)
 
RBAC: access denied
 => Her şey yolunda ama yetkisi yok request atmaya
