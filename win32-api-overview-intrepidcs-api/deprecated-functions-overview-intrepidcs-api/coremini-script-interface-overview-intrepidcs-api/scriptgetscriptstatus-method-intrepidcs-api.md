# ScriptGetScriptStatus Method - intrepidcs API

This method returns the status of the script on a neoVI device.

{% tabs %}
{% tab title="C/C++ Declare" %}
```
int _stdcall icsneoScriptGetScriptStatus(void * hObject, unsigned int iFunctionBlockIndex, int *piStatus);
```
{% endtab %}

{% tab title="Visual Basic .NET Declare" %}
```
Public Declare Function icsneoScriptGetScriptStatus Lib “icsneo40.dll” (ByVal hObject As IntPtr, ByRef piStatus As Int32) As Int32
```
{% endtab %}

{% tab title="C# Declare" %}
```
[DllImport(“icsneo40.dll”)] public static extern Int32 icsneoScriptGetScriptStatus(IntPtr hObject, ref Int32 piStatus);
```
{% endtab %}
{% endtabs %}

**Parameters**

hObject

\[in] Specifies the driver object created by OpenNeoDevice.

iFunctionBlockIndex

\[in] The index value of the function block

piStatus

\[out] 0 = Stopped 1 = Running

**Return Values**

1 if the function succeeded. 0 if it failed for any reason. GetLastAPIError must be called to obtain the specific error. The errors that can be generated by this function are:

NEOVI\_ERROR\_DLL\_SCRIPT\_NO\_SCRIPT\_RUNNING = 226

**Remarks**

The script must have been successfully downloaded to the neoVI using ScriptLoadScript.

### Examples

{% tabs %}
{% tab title="C/C++ Example:" %}
```cpp
int iRetVal;
int iStatus;
unsigned long lLastErrNum;

iRetVal = icsneoScriptGetScriptStatus(hObject, &iStatus);
if(iRetVal == 0)
{
    printf("\nFailed to get the script status. API Error = %d\r\n", lLastErrNum);
}
else
{
    printf("\nScript status = %s\r\n", iStatus == 0 ? "Stopped" : "Running");
}
```
{% endtab %}

{% tab title="C# Example:" %}
```csharp
Int32 iResult;
Int32 iStatus=0;

//Get CoreMini Status
iResult = icsNeoDll.icsneoScriptGetScriptStatus(m_hObject,ref iStatus);

if (iResult == 0)
{
    lblCMStatus.Text = "Failed to get CoreMini Status";
}
else
{
    switch(iStatus)
    {
        case (int)ScriptStates.SCRIPT_STATUS_RUNNING:
            lblCMStatus.Text = "CoreMini Script Running";
            break;
        case (int)ScriptStates.SCRIPT_STATUS_STOPPED:
            lblCMStatus.Text = "CoreMini Script Stopped";
            break;
        default:
            lblCMStatus.Text = "Unhandled State";
            break;
    }
}
```
{% endtab %}

{% tab title="Visual Basic .NET Example:" %}
```vbnet
Dim iResult As Int32
Dim iStatus As Int32

'//Get CoreMini Status
iResult = icsneoScriptGetScriptStatus(m_hObject, iStatus)

If iResult = 0 Then
    lblCMStatus.Text = "Failed to get CoreMini Status"
Else
    Select Case iStatus
        Case SCRIPT_STATUS_RUNNING
            lblCMStatus.Text = "CoreMini Script Running"
        Case SCRIPT_STATUS_STOPPED
            lblCMStatus.Text = "CoreMini Script Stopped"
        Case Else
            lblCMStatus.Text = "Unhandled State"
    End Select
End If
```
{% endtab %}
{% endtabs %}
