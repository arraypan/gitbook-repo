# WaitForRxMessagesWithTimeOut Method - intrepidcs API

This method is used to wait a specified amount of time for received messages from the neoVI hardware.

{% tabs %}
{% tab title="C/C++ Declare" %}
```cpp
int _stdcall icsneoWaitForRxMessagesWithTimeOut(void * hObject, unsigned int iTimeOut);
```
{% endtab %}

{% tab title="Visual Basic .NET Declare" %}
```vbnet
Public Declare Function icsneoWaitForRxMessagesWithTimeOut Lib “icsneo40.dll” (ByVal hObject As IntPtr, ByVal iTimeOut As UInt32) As Int32
```
{% endtab %}

{% tab title="C# Declare" %}
```csharp
[DllImport(“icsneo40.dll”)] public static extern Int32 icsneoWaitForRxMessagesWithTimeOut(IntPtr hObject, UInt32 iTimeOut);
```
{% endtab %}
{% endtabs %}

**Parameters**

hObject

\[in] Specifies the driver object created by OpenNeoDevice.

iTimeOut

\[in] Specifies the amount of time in milliseconds that the function will wait for a received message before returning.

**Return Values**

0 if no message was received during the wait period. 1 if a message was received. -1 will be returned if there is an error condition. GetLastAPIError must be called to obtain the specific error. The errors that can be generated by this function are:

NEOVI\_ERROR\_DLL\_NEOVI\_NO\_RESPONSE = 75

**Remarks**

This function allows an application to avoid ‘polling’ for received messages. It will return as soon as a message is received or when the timeout specified has been reached.

### **Examples**

{% tabs %}
{% tab title="C/C++ Example" %}
```cpp
void * hObject = 0; // holds a handle to the neoVI object
icsSpyMessage stMessages[19999]; // holds the received messages
int iResult;
int iNumberOfErrors;
int iNumberOfMessages;
unsigned int iTimeOut = 5; //milliseconds
bool bDone = false;

while(!bDone)
{
    iResult = icsneoWaitForRxMessagesWithTimeOut(hObject, iTimeOut);

    if(iResult == 0)
        continue; //no messages received

    iResult = icsneoGetMessages(hObject,stMessages,&iNumberOfMessages,&iNumberOfErrors);

    if(iResult == 0)
        MessageBox(hWnd,TEXT("Problem Reading Messages"),TEXT("neoVI Example"),0);
    else
        MessageBox(hWnd, TEXT("Messages Read Successfully"),TEXT("neoVI Example"),0);
}

return 0;
```
{% endtab %}

{% tab title="Visual Basic .NET Example" %}
```vbnet
Private m_hObject As IntPtr '// Declared at form level and previously open with a call to OpenNeoDevice

Dim iResult As Integer
Dim iTimeOut As UInt32

iTimeOut = Convert.ToUInt32(5000)

lblWaitForRxMessageWithTimeOutResult.Text = "Status"
Application.DoEvents()

'//This function will block until, A: A Message is received by the hardware, or B: the timeout is reached
iResult = icsneoWaitForRxMessagesWithTimeOut(m_hObject, iTimeOut)
If iResult = 1 Then
    'Message received before timeout
    lblWaitForRxMessageWithTimeOutResult.Text = "Message received"
    Call cmdReceive_Click(sender, e)
    '//Do something with the messages received
Else
    'Timeout reached and no messages received
    lblWaitForRxMessageWithTimeOutResult.Text = "Message Not received"
    '//Take action if no messages were received
End If
```
{% endtab %}

{% tab title="C# Example" %}
```csharp
//Declared at form level and previously open with a call to OpenNeoDevice
IntPtr m_hObject; //handle for device

int iResult;
UInt32 iTimeOut = 5000; //Set timeout to 5 seconds

lblWaitForRxMessageWithTimeOutResult.Text = "Status";
Application.DoEvents();

//This function will block until, A: A Message is received by the hardware, or B: the timeout is reached
iResult = icsNeoDll.icsneoWaitForRxMessagesWithTimeOut(m_hObject, iTimeOut);
if (iResult == 1)
{
    //Message received before timeout
    lblWaitForRxMessageWithTimeOutResult.Text = "Message received";
    //Do something with the messages received
    cmdReceive_Click(sender, e);
}
else
{
    //Timeout reached and no messages received
    lblWaitForRxMessageWithTimeOutResult.Text = "Message Not received";
    //Take action if no messages were received
}
```
{% endtab %}
{% endtabs %}