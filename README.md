![image](https://github.com/8338/Gui-ToolBox/assets/61122684/eb9527de-c477-4e2a-bf2d-75547bc5f717)

# Gui-ToolBox

Add-Type -AssemblyName System.Windows.Forms

$FormObject=[System.Windows.Forms.Form]
$LabelObject=[System.Windows.Forms.Label]
$ComboBoxObject=[System.Windows.Forms.ComboBox]
$ButtonObject=[System.Windows.Forms.Button]
$computerName=[System.Environment]::MachineName

#GUI COLOR dark light scheme
$scheme = 'dark'

#gui
$AppForm=New-Object $FormObject
$AppForm.ClientSize='400,700'
$AppForm.Text='ToolBOX                                        User :',$computerName

if ($scheme -eq 'dark') {
    $AppForm.BackColor='#000000'
} else {
    $AppForm.BackColor='#ffffff'
}

#gui no resize
$AppForm.FormBorderStyle ='FixedDialog'
$Appform.MaximizeBox = $false

#Loggide text box
$logBox=New-Object $LabelObject #system.Windows.Controls.TextBox
$logBox.Text='LOGGID'
$logBox.Size='360,80'
$logBox.BackColor='#2D2E40'
$logBox.Location=New-Object System.Drawing.Point(20,600)

#formi ehitus
$Sysinfo=New-Object $LabelObject
$Sysinfo.Text='Tools :'
$Sysinfo.AutoSize=$true
$Sysinfo.ForeColor='#ffffff'
$Sysinfo.Location=New-Object System.Drawing.Point(20,20)

# Light, Dark theme
$schemeButton = New-Object $ButtonObject
$schemeButton.Text = '  '
$schemeButton.Location = New-Object System.Drawing.Point(380,0)
$schemeButton.Size = New-Object System.Drawing.Size(20,20)
$schemeButton.Add_Click({
    if ($scheme -eq 'dark') {
        $script:scheme = 'light'
        $AppForm.BackColor='#ffffff'
        $logBox.BackColor='#f0f0f0'
        $Sysinfo.ForeColor='#000000'
    } else {
        $script:scheme = 'dark'
        $AppForm.BackColor='#000000'
        $logBox.BackColor='#2D2E40'
        $Sysinfo.ForeColor='#ffffff'
    }
    $AppForm.Refresh()
})

#Search
$ddlService=New-Object $ComboBoxObject
$ddlService.Width='300'
$ddlService.Location=New-Object System.Drawing.Point(70,15)

# Add items to the ComboBox
$ddlService.Items.Add("System Info")
$ddlService.Items.Add("Tab 2")
$ddlService.Items.Add("Tab 3")
$ddlService.Items.Add("Tab 4")
$ddlService.Items.Add("Tab 5")

# Set the selected item
$ddlService.SelectedItem = "Tab 1"

$AppForm.Controls.AddRange(@($Sysinfo,$logBox,$schemeButton,$ddlService))

#N2itab forme
$AppForm.ShowDialog()

##prugi
$AppForm.Dispose()
