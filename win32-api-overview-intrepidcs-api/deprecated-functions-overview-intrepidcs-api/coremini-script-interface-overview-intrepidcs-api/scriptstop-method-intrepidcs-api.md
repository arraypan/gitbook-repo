# ScriptStop Method - intrepidcs API

This method stops the execution of a script that is running on a neoVI device.

{% tabs %}
{% tab title="C/C++ Declare" %}
```
int _stdcall icsneoScriptStop(void * hObject);
```
{% endtab %}

{% tab title="Visual Basic .NET Declare" %}
```
Public Declare Function icsneoScriptStop Lib “icsneo40.dll” (ByVal hObject As IntPtr) As Int32
```
{% endtab %}

{% tab title="C# Declare" %}
```
[DllImport(“icsneo40.dll”)] public static extern Int32 icsneoScriptStop(IntPtr hObject);
```
{% endtab %}
{% endtabs %}

**Parameters**

hObject

\[in] Specifies the driver object created by OpenNeoDevice.

**Return Values**

1 if the function succeeded. 0 if it failed for any reason. GetLastAPIError must be called to obtain the specific error.

**Remarks**

If a script is executing on the neoVI calling this method will stop it. The script will still be present on the device and can be started again by ScriptStart The errors that can be generated by this function are:

NEOVI\_ERROR\_DLL\_NEOVI\_NO\_RESPONSE = 75

NEOVI\_ERROR\_DLL\_SCRIPT\_NO\_SCRIPT\_RUNNING = 226

### Examples

{% tabs %}
{% tab title="C/C++ Example:" %}
```cpp
int iRetVal;
unsigned long lLastErrNum;

iRetVal = icsneoScriptStop(m_hObject);
if(iRetVal == 0)
{
    printf("Failed to Stop the script API Error\n");
}
else
{
    printf("Successfully stopped the script\n");
}
```
{% endtab %}

{% tab title="C# Example:" %}
```csharp
Int32 iResult;

//Stop CoreMini
iResult = icsNeoDll.icsneoScriptStop(m_hObject);

if(iResult == 0)
{
    lblCMStatus.Text = "CoreMini Failed to Stop";
}
else
{
    lblCMStatus.Text = "CoreMini Stopped";
}
```
{% endtab %}

{% tab title="Visual Basic .NET Example:" %}
```vbnet
Dim iResult As Int32

'//Stop CoreMini
iResult = icsneoScriptStop(m_hObject)

If iResult = 0 Then
    lblCMStatus.Text = "CoreMini Failed to Stop"
Else
    lblCMStatus.Text = "CoreMini Stopped"
End If
```
{% endtab %}
{% endtabs %}
