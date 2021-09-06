# CS_mock
模拟cobalt strike beacon上线包.  Simulation cobalt strike beacon connection packet.

拿到c2通信使用的RSA public key和提交metedata的url 即可模拟上线

Use the CobaltStrikeParser extract public key from the payload https://github.com/Sentinel-One/CobaltStrikeParser  parse_beacon_config.py payload_url --json

Remember to remove the extra padding from the public key
![](CSMOCK.png)


### 0x01 nmap scan from c2 server

`$ cScan 10.10.26.164 80`

```
Nmap scan report for 10.10.26.164
Host is up (0.0019s latency).

PORT   STATE SERVICE
80/tcp open  http
| grab_beacon_config_rsa:
|   x86:
|     time: 1630913440646.5
|     sha256: e85b3ab8b81cf843b02b8c4e2a25766cd1ccc347dfa48e9ede3f1f128aad5ff7
|     config:
|       RSA Public Key: MIGfMA0GCSqGSIb3DQEBAQUAA4GNADCBiQKBgQCoeNuV/KkCl7dHwdyl8CIn1o5nHvVxquEs3k58509cojk+arW8dSzfPa2eVrjHtc4rMd7WGLif4AA9FaBwHgIdZ8J9K4xU1V9wWxF6iIFHcOT04KcFdZnJ4nXgMFrI7j4TYK1ugS9qV8u7C3Necrl38vRvOPi0kMYMiRO5KtT0KwIDAQAB
|       Jitter: 0
|       C2 Server: 10.10.26.164,/load
|       Spawn To x64: %windir%\sysnative\rundll32.exe
|       C2 Host Header:
|       Polling: 60000
|       Port: 80
|       Watermark: 1234567890
|       Method 2: POST
|       Method 1: GET
|       HTTP Method Path 2: /submit.php
|       Spawn To x86: %windir%\syswow64\rundll32.exe
|       Beacon Type: 0 (HTTP)
|     md5: 20e1378670b0d882f8ffb4e5e3ee0d9d
|     uri_queried: /HjIa
|     sha1: 48aecd9afe30e2dcafc456cbe4cd5fa2986c2217
|   x64:
|     time: 1630913441918.8
|     sha256: f4e4f1f97aed0eea7ddaf2d3c5b60005fac38befba13d0804732e45eecec22fd
|     config:
|       RSA Public Key: MIGfMA0GCSqGSIb3DQEBAQUAA4GNADCBiQKBgQCoeNuV/KkCl7dHwdyl8CIn1o5nHvVxquEs3k58509cojk+arW8dSzfPa2eVrjHtc4rMd7WGLif4AA9FaBwHgIdZ8J9K4xU1V9wWxF6iIFHcOT04KcFdZnJ4nXgMFrI7j4TYK1ugS9qV8u7C3Necrl38vRvOPi0kMYMiRO5KtT0KwIDAQAB
|       Jitter: 0
|       C2 Server: 10.10.26.164,/__utm.gif
|       Spawn To x64: %windir%\sysnative\rundll32.exe
|       C2 Host Header:
|       Polling: 60000
|       Port: 80
|       Watermark: 1234567890
|       Method 2: POST
|       Method 1: GET
|       HTTP Method Path 2: /submit.php
|       Spawn To x86: %windir%\syswow64\rundll32.exe
|       Beacon Type: 0 (HTTP)
|     md5: 8478e44aff0b52772697f5bfcf4e24b0
|     uri_queried: /4Ovd
|_    sha1: c6bdfdacd266e6024da8cccd7c7b251bad247e3f

Nmap done: 1 IP address (1 host up) scanned in 3.41 seconds

```

RSA Public Key 

```
MIGfMA0GCSqGSIb3DQEBAQUAA4GNADCBiQKBgQCoeNuV/KkCl7dHwdyl8CIn1o5nHvVxquEs3k58509cojk+arW8dSzfPa2eVrjHtc4rMd7WGLif4AA9FaBwHgIdZ8J9K4xU1V9wWxF6iIFHcOT04KcFdZnJ4nXgMFrI7j4TYK1ugS9qV8u7C3Necrl38vRvOPi0kMYMiRO5KtT0KwIDAQAB
```

### c2-profile

```
header = {
        'Cookie': "__cfduid=" + base64.b64encode(enpack).decode('utf-8')
    }
```

#### Default:

```
GET /jquery-3.3.1.min.js HTTP/1.1
Accept-Encoding: identity
Host: 10.10.26.164
User-Agent: Python-urllib/3.9
Cookie: od8aPOC86rrPtnIJVmt5a4VjQMyjjzZxZrtuU2sOlGVZvO08c6od6PIjoS65qPrrX7Op036kjBB4QmAJd5pJUvGXpOYRB02v7reZZdAwpPEWwaxxUJxDBWovNcfYexw5dgCrbpVv/kKnAuemh1JYrAaYyvikRJvBrgQzjcOBBJM=
```

#### Cookie cfduid
```
GET /jquery-3.3.1.min.js HTTP/1.1
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Referer: http://code.jquery.com/
Accept-Encoding: gzip, deflate
Cookie: __cfduid=e4kfutNGa060S9mZiqDfitie2GtdNNctRVVxSktYsgO7mQ-w5QEAlr_PZVzr-U4NYky9FTh1-fMGvi1Jjm7bQRpQrhUR4Et0CSWcFQK9fn0RqKJp6oREleOddJ9avbI9PLZQHzIBqo1qfgCYrGsGvRMBn90usUMOK4cDjQ6UF24
User-Agent: Mozilla/5.0 (Windows NT 6.3; Trident/7.0; rv:11.0) like Gecko
Host: 10.10.26.164
Connection: Keep-Alive
Cache-Control: no-cache
```



