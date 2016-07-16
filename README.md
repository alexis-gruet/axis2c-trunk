# axis2c-trunk
Mirror of axis2/c

#Ubuntu 14.04-LTS

```
sudo apt-get install libjson0-dev 

./autogen.sh
./configure --enable-openssl=yes --with-openssl=/usr/include/openssl --disable-libxml2 --enable-guththila=yes --enable-json=yes --enable-trace=yes --enable-tcp --with-json="/usr/include/json-c"

make && make install
```

Axis2.xml
```
<axisconfig name="Axis2/C">
    <!-- ================================================= -->
    <!-- Parameters -->
    <!-- ================================================= -->
    <!-- Uncomment following to enable MTOM support -->
    <!--parameter name="enableMTOM" locked="false">true</parameter-->

    <!-- Set the suitable size for optimum memory usage when sending large attachments -->
    <!--parameter name="MTOMBufferSize" locked="false">10</parameter-->
    <!--parameter name="MTOMMaxBuffers" locked="false">1000</parameter-->
    <!--parameter name="attachmentDIR" locked="false">/path/to/the/attachment/caching/dir/</parameter-->
    <!-- Enable REST -->
    <parameter name="enableREST" locked="false">true</parameter>
  
    <!-- Uncomment following to persist op_ctx, useful with RM -->
    <parameter name="persistOperationContext" locked="false">true</parameter>

    <!--if you want to extract the service archive file and work with that please uncomment this-->
    <!--else , it wont extract archive file or does not take into consideration if someone drop-->
    <!--exploded directory into /service directory-->
    <!--<parameter name="extractServiceArchive" locked="false">true</parameter>-->


    <!-- ================================================= -->
    <!-- Message Receivers -->
    <!-- ================================================= -->
    <!-- This is the Deafult Message Receiver for the Request Response style Operations -->
    <!--messageReceiver mep="INOUT" class="axis2_receivers"/-->

    <!-- ================================================= -->
    <!-- Transport Ins -->
    <!-- ================================================= -->
    <transportReceiver name="http" class="axis2_http_receiver">
        <parameter name="port" locked="false">6060</parameter>
    </transportReceiver>

    <transportReceiver name="https" class="axis2_http_receiver">
        <parameter name="port" locked="false">6060</parameter>
    </transportReceiver>
    <!--transportReceiver name="tcp" class="axis2_tcp_receiver">
    <parameter name="port" locked="false">6060</parameter>
    </transportReceiver-->

    <!--<transportReceiver name="soap.udp" class="axis2_udp_receiver">-->
      <!--<parameter name="port" locked="false">6060</parameter>-->
      <!--Maximum UDP packet that can be received-->
      <!--<parameter name="UDPMaxPacketSize">16384</parameter>-->
      <!--If specified, receiver will join this multicast group-->
      <!--<parameter name="multicastGroup">239.255.255.250</parameter>-->
    <!--</transportReceiver>-->
    
    <!-- ================================================= -->
    <!-- Transport Outs -->
    <!-- ================================================= -->

    <transportSender name="http" class="axis2_http_sender">
        <parameter name="PROTOCOL" locked="false">HTTP/1.1</parameter>
      <parameter name="xml-declaration" insert="false"/>
      <!--parameter name="Transfer-Encoding">chunked</parameter-->
      <!--parameter name="PROXY" proxy_host="127.0.0.1" proxy_port="8080" locked="true"/-->
    </transportSender>

    <transportSender name="https" class="axis2_http_sender">
      <parameter name="PROTOCOL" locked="false">HTTP/1.1</parameter>
      <parameter name="xml-declaration" insert="false"/>
    </transportSender>
  
    <!--<transportSender name="soap.udp" class="axis2_udp_sender">-->
      <!--Following parameters are specified in the SOAP over UDP spec. User can change the values to suite their needs-->
      <!--<parameter name="uniRepeat">2</parameter>-->
      <!--<parameter name="uniMinDelay">50</parameter>-->
      <!--<parameter name="uniMaxDelay">250</parameter>-->
      <!--<parameter name="uniUpperDelay">500</parameter>-->
      <!--<parameter name="mulRepeat">4</parameter>-->
      <!--<parameter name="mulMinDelay">50</parameter>-->
      <!--<parameter name="mulMaxDelay">250</parameter>-->
      <!--<parameter name="mulUpperDelay">500</parameter>-->
      <!--Timeout for the single channel blocking case-->
      <!--<parameter name="timeOut">30</parameter>-->
      <!--Set the maximum packet size to be sent-->
      <!--<parameter name="UDPMaxPacketSize">16384</parameter>-->
    <!--</transportSender>-->
  
    <!--
    <parameter name="SERVER_CERT">/path/to/ca/certificate</parameter>
    <parameter name="KEY_FILE">/path/to/client/certificate/chain/file</parameter>
    <parameter name="SSL_PASSPHRASE">passphrase</parameter>
    -->

    <!-- ================================================= -->
    <!-- Global Modules  -->
    <!-- ================================================= -->
    <!-- Comment this to disable Addressing -->
    <module ref="addressing"/>
    <!--module ref="statistics"/-->
    <!--module ref="bam_publisher"/-->


    <!--Configuring module , providing paramters for modules whether they refer or not-->
    <!--<moduleConfig name="addressing">-->
    <!--<parameter name="addressingPara" locked="false">N/A</parameter>-->
    <!--</moduleConfig>-->

    <!-- ================================================= -->
    <!-- Phases  -->
    <!-- ================================================= -->
    <phaseOrder type="inflow">
        <!-- System pre defined phases       -->
        <phase name="Transport"/>
        <phase name="PreDispatch"/>
        <phase name="Dispatch"/>
        <phase name="PostDispatch"/>
        <!-- End system pre defined phases       -->
        <!-- After PostDispatch phase, module or service author can add any phase as required  -->
        <!-- User defined phases could be added here -->
	<phase name="Security"/>
        <phase name="Rahas"/>
	<phase name="RMPhase"/>
	<phase name="OpPhase"/>
	<phase name="SavanPhase"/>
    </phaseOrder>
    <phaseOrder type="outflow">
        <!-- User defined phases could be added here -->
        <phase name="RMPhase"/>
	<phase name="OpPhase"/>
		<phase name="SavanPhase"/>
	<!--phase name="userphase1"/-->
        <!--system predefined phase-->
        <phase name="MessageOut"/>
        <phase name="Security"/>
    </phaseOrder>
    <phaseOrder type="INfaultflow">
        <!-- User defined phases could be added here -->
        <!--phase name="userphase1"/-->
	<phase name="RMPhase"/>
	<phase name="OpPhase"/>
		<phase name="SavanPhase"/>
    </phaseOrder>
    <phaseOrder type="Outfaultflow">
        <!-- User defined phases could be added here -->
        <phase name="RMPhase"/>
	<!--phase name="userphase1"/-->
        <phase name="SavanPhase"/>
        <phase name="MessageOut"/>
    </phaseOrder>
</axisconfig>
```
