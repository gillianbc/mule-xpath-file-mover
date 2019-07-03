This is a simple flow that listens for xml files arriving in the data/in folder, parses the contents and detects whether the carrier is UPS, FedEx or other.


Tutorial from article https://blogs.mulesoft.com/dev/anypoint-platform-dev/using-xpath-expressions-on-an-xml-document-with-namespaces/

The file contents use a namespace xmlns="http://checkout.google.com/schema/2 which means all element names within that file belong to that namespace by default.

Therefore, when we are looking for elements in an xpath expression, we need to use that namespace.

We use the name space manager:

<mulexml:namespace-manager doc:name="Declare Namespace alias">
    <mulexml:namespace prefix="gco" uri="http://checkout.google.com/schema/2"/>
</mulexml:namespace-manager>

The namespace manager is declared outside of the flow (you can't put it in a flow).

To use the namespace manager, you must declare it's namespace - I've called it mulexml, but could be anything.  You also need to declare the schema.  I'm using xpath3 hence 'current' in the schema path.  This wasn't available in the earlier releases e.g. http://www.mulesoft.org/schema/mule/file/3.1/mule-file.xsd"

xmlns:file="http://www.mulesoft.org/schema/mule/file"
xmlns="http://www.mulesoft.org/schema/mule/core" 
xmlns:doc="http://www.mulesoft.org/schema/mule/documentation"
xmlns:spring="http://www.springframework.org/schema/beans" 
xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
xmlns:mulexml="http://www.mulesoft.org/schema/mule/xml"
xsi:schemaLocation=
"http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans-current.xsd
http://www.mulesoft.org/schema/mule/core http://www.mulesoft.org/schema/mule/core/current/mule.xsd
http://www.mulesoft.org/schema/mule/xml http://www.mulesoft.org/schema/mule/xml/current/mule-xml.xsd
http://www.mulesoft.org/schema/mule/file http://www.mulesoft.org/schema/mule/file/current/mule-file.xsd">

To see the app in action, drop some xml files into the data/in folder.  
The xml is parsed, you'll see log messages and the file is then moved to the data/processed folder.


