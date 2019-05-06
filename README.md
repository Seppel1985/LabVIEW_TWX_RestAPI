# LabVIEW_TWX_RestAPI
The project provides LabVIEW Snippets to connect via REST calls to Thingworx

The repository consists of 2 Folders.
One folder is the "ThingworxObjects" folder, which contains a XML-Export with 3 Thingworx entities used by the LabVIEW demo.
* Thingworx Entities:
  * Project: LabViewDemo
  * Thing: LabviewTestObject - Has 2 properties defined and a service, to be used in the demo.
  * ApplicationKey: MyAdminAppKey - Used to authenticate against Thingworx, assigned to Administrator.
  
*Note: Assigning an AppKey to Administrator is not recommended!*

The other folder "LabviewVIs", contains a set of Labview VIs.
* VIs:
  * DemoVI_Thingworx.vi: Contains a Demo, using all SubVIs and performs GET, POST and PUT calls against TWX.
  * Init HTTP (SubVI).vi: Creates an HTTP handle, by applying the right header data<br/>
  ![Image of Init HTTP](https://github.com/Seppel1985/LabVIEW_TWX_RestAPI/blob/master/images/INIT.png)
  	* Input: 	
		* Application Key - Thingworx AppKey to Authenticate
	* Output:	
		* Refnum - contains a pointer with the http handle
		* Error Out - contains the Error cluster, which keeps track of errors during execution
  * Send HTTP (SubVI).vi: Sends based on the input cluster an HTTP Request with GET, POST, PUT or DELETE
  ![Image of Send HTTP](https://github.com/Seppel1985/LabVIEW_TWX_RestAPI/blob/master/images/SEND.png)
    * Input: 	
		* Thingworx Server Information Cluster - contains all Information to connect to Thingworx incl. AppKey, ServerAddr, TWX-Object, HTTP request method
		* Refnum - contains a pointer with the http handle
		* Error - contains the Error cluster, which keeps track of errors during execution
	* Output:	
		* HTTP Response Header - information available as string
		* HTTP Response Body - information available as string
		* Refnum - contains a pointer with the http handle
		* Error - contains the Error cluster, which keeps track of errors during execution
  * Close HTTP (SubVI).vi: Closes the HTTP handle, which will be provided as Input<br/>
  ![Image of Close HTTP](https://github.com/Seppel1985/LabVIEW_TWX_RestAPI/blob/master/images/CLOSE.png)
    * Input: 	
		* Refnum - contains a pointer with the http handle
		* Error - contains the Error cluster, which keeps track of errors during execution
	* Output:	
		* Error - contains the Error cluster, which keeps track of errors during execution
  * ErrorCodes (SubVI).vi: Analysis the header response of the HTTP call and provides TWX specific error notifications<br/>
  ![Image of ErrorCodes](https://github.com/Seppel1985/LabVIEW_TWX_RestAPI/blob/master/images/ERROR.png)
    * Input: 	
		* HTTP Header Response (String) - contains the header response of the http call
		* Error - contains the Error cluster, which keeps track of errors during execution
	* Output:	
		* Error - contains the Error cluster, which keeps track of errors during execution
  * Helper_JSON (SubVI).vi: Parses the TWX JSON answer down to a specific text field - by default rows[0].result<br/>
  ![Image of Helper_JSON](https://github.com/Seppel1985/LabVIEW_TWX_RestAPI/blob/master/images/Helper_JSON.png)
    * Input: 	
		* HTTP Response Body - JSON response coming from Thingworx system
		* Outer JSON - as TWX usually answers with a nested JSON, it is possible to extract data by navigating to the Outer JSON and then the Inner JSON. The outer JSON is usually named rows, whilst the inner JSON depends on variable names
		* Inner JSON - Name for the inner JSON - after rows[0].
		* Error - contains the Error cluster, which keeps track of errors during execution
	* Output:	
		* Error - contains the Error cluster, which keeps track of errors during execution
  * Helper_DATE (SubVI).vi: Converts from the labview date format (time since 1/1/1904 in sec) into the TWX timestamp format (unix timestamp in ms)<br/>
  ![Image of Helper_DATE](https://github.com/Seppel1985/LabVIEW_TWX_RestAPI/blob/master/images/Helper_Date.png)
    * Input: 	
		* Timestamp - Timestamp produced by Labview (seconds since 1/1/1904 until chosen date)
	* Output:	
		* TWX Timestamp - milliseconds since 1/1/1970 until chosen date

