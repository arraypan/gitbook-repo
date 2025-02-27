# GetDeviceSettings Method - intrepidcs API

This method reads the configuration settings from various devices.

{% tabs %}
{% tab title="C/C++ Declare" %}
```
int _stdcall icsneoGetDeviceSettings(void * hObject, SDeviceSettings *pSettings, int iNumBytes, int VnetChan);
```
{% endtab %}

{% tab title="Visual Basic .NET Declare" %}
```
Public Declare Function icsneoGetDeviceSettingsLib “icsneo40.dll” (ByVal hObject As IntPtr, ByRef pSettings As SDeviceSettings , ByVal iNumBytes As Int32, ByVal VnetChan As Int32) As Int32
```
{% endtab %}

{% tab title="C# Declare" %}
```
[DllImport(“icsneo40.dll”)] public static extern Int32 icsneoGetDeviceSettings(IntPtr hObject, rref SDeviceSettings pSettings, Int32 iNumBytes, Int32 VnetChan);
```
{% endtab %}
{% endtabs %}

**Parameters**

hObject

\[in] Specifies the driver object created by OpenNeoDevice.

pSettings

\[out] Pointer to a SDeviceSettings structure.

iNumBytes

\[in] This value is always the size, in bytes, of the SDeviceSettings structure.

VnetChan

\[in] This value is indicates which Vnet to set the settings to. This parameter is intended for neoVI ION and neoVI Plasma which have more than one Vnet Slot. For all other devices set this to 0.

**Return Values**

Returns 1 if successful, 0 if an error occurred. GetLastAPIError must be called to obtain the specific error. The errors that can be generated by this function are:

NEOVI\_ERROR\_DLL\_NEOVI\_NO\_RESPONSE = 75

**Remarks**

After getting the current settings, you may change the parameters defined in the SDeviceSettings structure and write the settings back to the neoVI FIRE 2 using SetDeviceSettings.

### Examples

{% tabs %}
{% tab title="C/C++ Example" %}
```
SDeviceSettings DeviceReadSettings;
int iNumberOfBytes;
int iResult;

//Get the settings
iNumberOfBytes=sizeof(DeviceReadSettings);
DeviceReadSettings.DeviceSettingType = DeviceFireSettingsType;
iResult = icsneoGetDeviceSettings(m_hObject, &DeviceReadSettings , iNumberOfBytes, 0);
if(iResult == 0)
{
    MessageBox::Show("Problem reading configuration");
    return;
}
```
{% endtab %}

{% tab title="C# Example" %}
```
SDeviceSettings DeviceReadSettings = new SDeviceSettings ();
int iNumberOfBytes;
int iResult;

//Get the settings
iNumberOfBytes = System.Runtime.InteropServices.Marshal.SizeOf(DeviceReadSettings);
DeviceReadSettings.uiDevice = EDeviceSettingsType.DeviceFireSettingsType;
iResult = icsNeoDll.icsneoGetDeviceSettings(m_hObject,ref DeviceReadSettings, iNumberOfBytes, 0);
if (iResult == 0)
{
    MessageBox.Show("Problem reading configuration");
    return;
}
```
{% endtab %}

{% tab title="Visual Basic .NET Example" %}
```
Dim DeviceReadSettings As SDeviceSettings
Dim iNumberOfBytes As Integer
Dim iResult As Integer

'//Get the settings
iNumberOfBytes = System.Runtime.InteropServices.Marshal.SizeOf(DeviceReadSettings)
DeviceReadSettings.uiDevice = EDeviceSettingsType.DeviceFireSettingsType
iResult = icsneoGetDeviceSettings(m_hObject, DeviceReadSettings, iNumberOfBytes, 0)
If iResult = 0 Then
    MsgBox("Problem reading configuration")
    Exit Sub
End If
```
{% endtab %}
{% endtabs %}
