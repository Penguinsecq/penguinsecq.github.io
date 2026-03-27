<h2>Check the Health of Windows System files</h2>

 <p>We are first going to do a quick scan of the Windows system:</p>	
 <pre><code>DISM /Online /Cleanup-Image /CheckHealth </code></pre> 

Advanced system scan 

  The next step is to do a more advanced system. ScanHealth will check the component store and report any corruption in the log file: C:\Windows\Logs\CBS\CBS.log

  DISM /Online /Cleanup-Image /ScanHealth
	

Repair Windows with DISM Online Cleanup Image Restorehealth 

	When the ScanHealth or CheckHealth commands found any corruption then we can repair it with the RestoreHealth command:

	DISM /Online /Cleanup-Image /RestoreHealth


Repair the current Windows Installation

Run the command below to repair the files:
sfc /scannow



Free up disk space with DISM

Analyze the Component Store
The first step is to analyze the Windows Update component store. The command below will go through all the update files to see what can be removed.
	1. Right-click on start (or press Windows key + X)
	2. Choose Windows PowerShell (admin) or Windows Terminal (admin)
	3. Enter the command below:
Dism /Online /Cleanup-Image /AnalyzeComponentStore


Cleanup old files manually

On Windows 10 you might not get the option to restart your computer. In this case, we will need to start the clean-up manually with the command below:
Dism /Online /Cleanup-Image /StartComponentCleanup
Once completed use the command below to reduce the size even further:
Dism /Online /Cleanup-Image /StartComponentCleanup /ResetBase
The ResetBase command can take some time, just let it complete.


Reference:
https://lazyadmin.nl

<img width="730" height="1195" alt="image" src="https://github.com/user-attachments/assets/82769f4e-8521-4a94-9939-dbc494ac6a64" />
