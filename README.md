# How to read WSDL? (UserInfoService.wsdl)


#### step1: Service : Service has reference to Port > Port has reference to Binding.

```
<wsdl:service name="UserInfoService"> //This is name of webservice.
    
    //This is description of web service.
    <wsdl:documentation> 
        This Service communicates with various backend systems like OVD, Samson, etc., to retrieve User details
    </wsdl:documentation>

    //Port is like an exposed URL. This referes binding information.
    <wsdl:port name="UserInfoServiceSOAPPort" binding="rsp:UserInfoServiceSOAPBinding"> 
        <soap:address location="http://localhost:8080/example/UserInfoService"/>
    </wsdl:port>

</wsdl:service>
```


#### step2: Binding : Binding has reference to PortType.


- **Note:** Binding is like category: which tells us the operations. We can have multilpe bindings, with operations in it.  
**Example:**
  - user-controller in swagger is "binding". 
  - 'getUsers' is an operation.
  - Similarly 'updateUsers' is an operation.

```
    <wsdl:binding name="UserInfoServiceSOAPBinding" type="rsp:UserInfoServicePortType">

        <soap:binding style="document" transport="http://schemas.xmlsoap.org/soap/http" />

        <wsdl:operation name="getUserInfo">
            <soap:operation soapAction="getUserInfo" />
            <wsdl:input><soap:body use="literal" /></wsdl:input>
            <wsdl:output><soap:body use="literal" /></wsdl:output>
        </wsdl:operation>

        <wsdl:operation name="updateUserInfo">
            <soap:operation soapAction="updateUserInfo" />
            <wsdl:input><soap:body use="literal" /></wsdl:input>
            <wsdl:output><soap:body use="literal" /></wsdl:output>
        </wsdl:operation>

    </wsdl:binding>
```

#### step3: PortType referes request and response messages.

- **Note:** Port type, makes operation to it's input and output assignments. I/O in an operation are assigned to messages.

```
    <wsdl:portType name="UserInfoServicePortType">

        <wsdl:operation name="getUserInfo">
            <wsdl:documentation>This operation retrieves the informations of an user from backend systems like OVD, Samson,etc</wsdl:documentation>
            <wsdl:input message="rsp:UserInfoRequestMessage" />
            <wsdl:output message="rsp:UserInfoResponseMessage" />
        </wsdl:operation>

        <wsdl:operation name="updateUserInfo">
            <wsdl:documentation>This operation updates specific fields associated with a Dealer code</wsdl:documentation>
            <wsdl:input message="rsp:UpdateUserInfoRequestMessage" />
            <wsdl:output message="rsp:UpdateUserInfoResponseMessage" />
        </wsdl:operation>

    </wsdl:portType>
```

#### step4: Messages referes to request/response objects.
- **Note:** Messages are like variables, which is assigned to specific object.

```
    <wsdl:message name="UserInfoRequestMessage">
        <wsdl:part name="UserInfoRequest" element="ns:userInfoRequest" />
    </wsdl:message>

    <wsdl:message name="UserInfoResponseMessage">
        <wsdl:part name="UserInfoResponse" element="ns:userInfoResponse" />
    </wsdl:message>

    <wsdl:message name="UpdateUserInfoRequestMessage">
        <wsdl:part name="UpdateUserInfoRequest" element="ns:updateUserInfoRequest" />
    </wsdl:message>

    <wsdl:message name="UpdateUserInfoResponseMessage">
        <wsdl:part name="UpdateUserInfoResponse" element="ns:updateUserInfoResponse" />
    </wsdl:message>
```


## soap service video tutorial

- How to understand WSDL?
- How to create SOAP request by WSDL? (Upload it to SOAPUI and you will get request)
- How to publish a local WSDL to live URL? (push WSDL file to github > raw text > link)
- How to view github WSDL in visualizer?
- How to generate WSDL files (in saperate directories) with - apache-codec-plugin?
- How to publish service with apache-cxf and jax-ws?