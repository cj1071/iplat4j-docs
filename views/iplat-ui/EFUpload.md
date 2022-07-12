## 自定义上传组件(IPLAT.FileUploader)

1. ### IPLAT.FileUploader

```javascript
IPLAT.FileUploader = function(options) {
	var element = $("#" + options.id);
	var saveUrl = IPLATUI.CONTEXT_PATH + "/XS/FA/XSFA4000.jsp?ename=" + options.ename + "&serviceName=" + options.serviceName + "&methodName=" + options.methodName; //文件导入后会跳转到这里指定到jsp，可增加自定义参数

	$.extend(options, {
		async: {
			saveUrl: saveUrl,
            success:function(result){},//上传成功回调
            error:function(e){}//上传失败回调
		}
	});
	return element.kendoUpload(options).data("kendoUpload");
};
```

2. ### [[EEDM0011-Excel导入数据](https://confluence.baocloud.cn/pages/viewpage.action?pageId=45297003)](https://confluence.baocloud.cn/pages/viewpage.action?pageId=45297003)

> ### CSTS05.jsp

```jsp
<EF:EFRegion id="ExcelImport " title="Excel导入 ">
    <EF:EFInput ename="fileForm" type="file"/>
</EF:EFRegion>
```
> ### 自定义封装IPLAT.FileUploader组件

```javascript
$(function() {

	IPLAT.FileUploader = function(options) {
		var element = $("#" + options.id);
		var saveUrl = IPLATUI.CONTEXT_PATH + "/XS/FA/XSFA4000.jsp?ename=" + options.ename + "&serviceName=" + options.serviceName + "&methodName=" + options.methodName; //文件导入后会跳转到这里指定到jsp，可增加自定义参数

		$.extend(options, {
			async: {
				saveUrl: saveUrl
			}
		});
		return element.kendoUpload(options).data("kendoUpload");
	};

	IPLAT.FileUploader({
		id: "fileForm",
		ename: "fileForm",
		serviceName: "CSTS05",
		methodName: "importForm"
	});
});
```

```java
<!--XSFA4000.jsp-->
<!--文件上传selvet转发页面，平台已实现，不需要添加-->

<%@ page contentType="text/html;charset=UTF-8" trimDirectiveWhitespaces="true" %>
<%@ page import="com.baosight.iplat4j.core.ei.EiConstant" %>
<%@ page import="com.baosight.iplat4j.core.ei.EiInfo" %>
<%@ page import="com.baosight.iplat4j.core.ioc.spring.PlatApplicationContext" %>
<%@ page import="com.baosight.iplat4j.core.log.LoggerFactory" %>
<%@ page import="com.baosight.iplat4j.core.service.soa.XLocalManager" %>
<%@ page import="org.springframework.web.multipart.MultipartHttpServletRequest" %>
<%@ page import="org.springframework.web.multipart.commons.CommonsMultipartResolver" %>
<%@ page import="java.util.Iterator" %>
<%@ page import="com.baosight.iplat4j.core.web.threadlocal.UserSession" %>
<%@ page import="com.baosight.iplat4j.core.exception.PlatException" %>
 
<%
    UserSession.web2Service(request);
    CommonsMultipartResolver multipartResolver = new CommonsMultipartResolver();
 
    String ename = request.getParameter("ename");
    String serviceName = request.getParameter(EiConstant.serviceName);
    String methodName = request.getParameter(EiConstant.methodName);
    MultipartHttpServletRequest multipartRequest = multipartResolver.resolveMultipart(request);
 
    // Iterator multiFileIterator = multipartRequest.getMultiFileMap().get(ename).iterator();
 
    // 反射 serviceName methodName
    EiInfo inInfo = new EiInfo();
    inInfo.set(EiConstant.serviceName, serviceName);
    inInfo.set(EiConstant.methodName, methodName);
    inInfo.set("multipartRequest", multipartRequest);
 
 
    inInfo.set("file", multipartRequest.getFileMap().get(ename));
 
    EiInfo outInfo = XLocalManager.call(inInfo);
    UserSession.getData().clear();
    if(outInfo.getStatus()<0){
        throw new PlatException(outInfo.getMsg());
    }
%>
```

> ### ServiceCSTS05.java
```java
public EiInfo importForm(EiInfo inInfo) throws IOException {
    MultipartFile file = (MultipartFile) inInfo.get("file");
   
    //根据业务需求，处理文件
  
    return inInfo;
}
```

